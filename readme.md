
#  Prerequisites #
To build a classifier, you must first have:

A valid Microsoft Account or an Azure Active Directory OrgID ("work or school account"), so you can sign into customvision.ai and get started. Note that OrgID login for AAD users from national clouds is not currently supported.
A series of images to train your classifier (minimum of 30 images per tag).
A few images to test your classifier after the classifier is trained.

# Getting Started: Build a Classifier # 
Custom Vision Service can be found by clicking here: https://customvision.ai

After you log into Custom Vision Service, you will be presented with a list of projects. You will be able to access your subscription keys once you have created your first project.


1. Click New Project to create your first project.
2. If this is your first project, you are asked to agree to the Terms of Service. Check the check box, then click the I agree button.

The New Project dialog box appears.
![New Project](https://i.imgur.com/S16E7wK.png)

Enter a name for this project, a description of the project, and select one domain.

| Domain        | Purpose           | 
| ------------- |-------------| 
| Generic     | If none of the other domains are appropriate, or you are unsure of which domain to choose, select the Generic domain. | 
| Food      | Optimized for photographs of dishes as you would see on a restaurant menu. If you want to classify photographs of individual fruits or vegetables, use the Generic domain for that purpose.  |  
| Landmarks | Optimized for recognizable landmarks, both natural and artificial. This domain works best when the landmark is clearly visible in the photograph, even if the landmark is slightly obstructed by a group of people posing in front of it.   | 
| Retail| Optimized for images found in a shopping catalog or shopping website. If you want high precision classifying between dresses, pants, and shirts, use this domain.  |
| Adult | Optimized to better define between adult content and non-adult content. For example, if you want to block images of people in bathing suits, this domain allows you to build a custom classifier to do that.|

**NOTE**: You can change the domain later if you want.

## Add images to train the classifier ##
Add some images to train your classifier. Let's say we want a classifier to distinguish between dogs, cats, and penguins. We need to upload and tag at least 30 images of dogs, 30 images of cats, and 30 images of ponies. You can get all of these from the pictures folder

**Note:** Custom Vision Service accepts training images in JPG/JPEG, PNG, and BMP format, up to 6 MB per image (prediction images can be up to 4 MB per image). Images are recommended to be 256 pixels on the shortest edge. Any images shorter than 256 pixels on the shortest edge will be scaled up by Custom Vision Service.
1. Click **Add images** 
![add images](https://i.imgur.com/OBUiZyR.png)
2. Browse to the images (you can multi-select)
 ![Browse](https://i.imgur.com/fzsTDeP.png)
3. Click `Open` to open the selected images
4. **Assign tags:** Type in the tag you want to assign, then press the **+** button to assign the tag. You can add more than one tag at a time to the images.
![tagging dogs](https://i.imgur.com/njRvxhA.png) 
5. When you are done adding tags, click **Upload [number] files**. The upload could take some time if you have a large number of images or a slow Internet connection. 
6. After the files have uploaded, click **Done**. 
![The progress bar shows all tasks completed. The upload report shows 38 images uploaded successfully. The Done button is on the lower right](https://i.imgur.com/PTX1KyX.png)
7. Repeat steps 1-7 with *cats* and *penguins*

## Train your classifier ##
After your images are uploaded, you are ready to train your classifier. All you have to do is click the **Train** button.
![](https://i.imgur.com/Hlxec6K.png)

This should only take a few minutes
![The train button is near the right top of the browser window.](https://i.imgur.com/cXIcXZN.png)


## Evaluate your classifier ##
The precision and recall indicators tell you how good your classifier is, based on automatic testing. Note that Custom Vision Service uses the images you submitted for training to calculate these numbers, using a process called [k-fold cross validation](https://en.wikipedia.org/wiki/Cross-validation_(statistics)).

![The training results, which shows the overall precision and recall, and the precision and recall for each tag in the classifier.](https://i.imgur.com/smZSycH.png)

**Note:** Each time you hit the "Train" button, you create a new iteration of your classifier. You can view all your old iterations in the Performance tab, and you can delete any that may be obsolete. When you delete an iteration, you end up deleting any images uniquely associated with it.

The classifier uses all the images to create a model that identifies each tag. To test the quality of the model, the classifier then tries each image on its model to see what the model finds.

The qualities of the classifier results are displayed

|Term|Definition|
|---|---|
|Precision|When you classify an image, how likely is your classifier to correctly classify the image? Out of all images used to train the classifier (dogs, cats, & penguins), what percent did the model get correct? 99 correct tags out of 100 images gives a Precision of 99%.|
|Recall|Out of all images that should have been classified correctly, how many did your classifier identify correctly? A Recall of 100% would mean, if there were 38 dog images in the images used to train the classifier, 38 dogs were found by the classifier.|


# Improve Your Classifier #

The quality of your classifier is foremost dependent on the quality of the labeled data you provide to it. 

1. The best way to have a quality classifier is to add more varied tagged images (different backgrounds, angles, object size, groups of photos, and variants of types.) Remember to train your classifier after you have added more images. Include images that are representative of what your classifier will encounter in the real world. Photos in context are better than photos of objects in front of neutral backgrounds, for example.

2. A core feature of Custom Vision Service is that images sent to your prediction endpoint are stored for you in the **Predictions** tab, so you can label them and use them to improve your classifier. Select an iteration from the left rail to see the images from that iteration. These images are ranked, so that the images that can bring the most gains to the classifier are at the top. Hover over an image to see predicted tags from your classifier. To tag an image, select one or more images and click "tag images". The images you have tagged will be moved to your **Training Images** tab. Remember to train after you are done tagging. 

   **Note:** The default view shows you images from the current iteration. You can drop down to find images submitted during previous iterations. 

   Tagging images from the **Predictions** tab is one of the best ways to improve your classifier. It is important to have your labeled training data to have similar properties to the data your classifier will encounter in the real world. Over time, consistent image tagging can help you improve your classifier.

3. Sometimes you can get a sense of how to improve your classifier by inspection. On the **Training Images** tab, you can see all your tagged images. On the left-rail if you select "Iteration History" and select an iteration, you can see a visual representation of which images were predicted correctly, and which were predicted incorrectly. Incorrect images (at your given Probability Threshold) and outlined with a red box to highlight them. Sometimes, by visual inspection, you can identify patterns that suggest what additional data you might want to label. For example, when building a “roses” vs “daises” classifier, if you notice all your white roses are labeled as daisies, your classifier may need more white roses in its training images. If artificially colored daises are labeled as roses, consider adding more of these daisies. 

4. Your classifier will learn characteristics that your photos have in common, not necessarily the characteristics you are thinking of. For example, if all your tulips were photographed outdoors in a field, and all the roses were photographed in front of a blue wall in a red vase, you have likely trained a field vs wall+vase classifier, not roses vs tulips. 

5. Custom Vision Service supports some automatic negative image handling. If you are building a “cat” vs “dog” classifier, and you submit an image of a shoe for prediction, Custom Vision Service should score that image as close to 0% for “cat” and 0% for “dog”. 

   **Note:** The automatic approach works for clearly negative images. It may not work well in cases where the negative images are just a variation of the images used in training. For example, if you have a “husky” vs “corgi” classifier, and you feed in an image of a Pomeranian, IRIS may score the Pomeranian as a Husky. If your negative images are of this nature, we recommend you create a new tag, such as “Other”, and apply it to your training images that are negative.


# Test and Retrain Your Model #
After you train your model, you can quickly test it using a locally stored image or an online image. The test uses the most recently trained iteration.

## Test your model ##

1. Click **Quick Test** on the right of the top menu bar. This action opens a window labeled **Quick Test**.

![The Quick Test button is shown in the upper right corner of the window.](https://i.imgur.com/67oBW6o.png)


2. In the **Quick Test** window, click in the **Submit Image** field and enter the URL of the image you want to use for your test. If you want to use a locally stored image instead, click the **Browse local files** button and select a local image file.

![The Quick Test window is shown. It has a URL field and a button for selecting local files.](https://i.imgur.com/Tn9a2pc.png)

The image you select appears in the middle of the page. Then the results appear below the image in the form of a table with two columns, labeled **Tags** and **Confidence**. After you view the results, you may close the **Quick Test** window.

You can now add this test image to your model and then retrain your model.

## Add a test image and retrain your model: ##

You can follow the steps below to add to your model an image that you have submitted for a quick test and to then retrain the model. However, adding only one image before you retrain your model doesn't lead to significant performance gains. For best results, add a significant number of images before you retrain the model.

1. Click the **PREDICTIONS** tab on the top menu bar.
2. Click the image you used for the quick test. A new window appears, with the image in the center.
3. In the new window, assign the correct tag to the image from the **My Tags** drop-down list. If you don't see the appropriate tag in the drop-down list, you can type in a new tag and then click the **+** sign to the right of the **My Tags** field.
4. Click the **Save and close** button at the bottom of the window.
4. Click the green **Train** button in the top menu bar.

# What's next #

[Use the Prediction Endpoint to Test Images Programmatically](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/use-prediction-api "Use the Prediction Endpoint to Test Images Programmatically")

[Export your model to mobilel](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/export-your-model "Export your model to mobile")