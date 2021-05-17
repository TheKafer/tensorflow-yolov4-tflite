# YOLO Network APP

<div align="center"><img src="/elementsReadme/galería.jpg" />
</div>

## ABOUT

This project is based on [amazing repository](https://github.com/hunglc007/tensorflow-yolov4-tflite), you are free to do whatever you want with this contribution.


## Motivation

This project was made with the objective of having an app for the detection of the leafminer pest in crops because they affect the production process of flowers in local crops. If you want to know more about our research you can read our [article](https://github.com/hunglc007/tensorflow-yolov4-tflite).

## Train your own model

### Images

If you are practicing you can use our own images or [these](https://drive.google.com/drive/folders/1dng7Noc7oc_QV6boHpCA7SphSLmayY0u?usp=sharing), make sure to classify them very well and divide them into folders for cross validation to evaluate your model.

### LabelImg

We recommend you to use  [labelImg](https://github.com/tzutalin/labelImg), this program makes your work much easier. Remember to change the format to yolo and be careful. Since this work is super important for your results.

![Error](/elementsReadme/labelImg.PNG?raw=true "LabelImg")

### Darknet 

Darknet is an optimized environment for the yolos network, in which we will generate the weights, you can use our [colab](https://colab.research.google.com/drive/1JQdI5WgmGbz4KBlbcwkUG9Q2fMStuuW1?usp=sharing) since we adapted it for your ease. We recommend you to read more about darknet. It is a bit complex at the beginning.

![Error](/elementsReadme/Darknet.PNG?raw=true "Darknet")

In the cfg folder is the configuration of your network, here you can change the parameters, the number of classes, modify layers, etc. In the img folder are the images for training and validation. Remember to upload the images with their files, you must have the same number of images and their respective files. After training your model, the weights will be saved in the weights folder.

Before implementing the app, test your weights. You can test them on darknet with videos or images.

![Error](/elementsReadme/res3.gif?raw=true "Darknet")

## Implement App

### Weight format

If you did not generate your own weights you can use [ours]([these](https://drive.google.com/drive/folders/1dng7Noc7oc_QV6boHpCA7SphSLmayY0u?usp=sharing)).

You must change the  `.weights` format to `.tflite`, because tflite is adapted to android. We recommend you to use this [amazing repository](https://github.com/hunglc007/tensorflow-yolov4-tflite)  to change the weights format.

Then you store the file `.tflite` on `.\android\app\src\main\assets`.

### Labels

Edit the file coco.txt on the folder `.\android\app\src\main\assets` and place the name of your classes.

### Change the code

In the file `\android\app\src\main\java\org\tensorflow\lite\examples\detection\DetectorActivity.java`, Adapt these lines to your needs.

```
    private static final int TF_OD_API_INPUT_SIZE = 416;
    private static final boolean TF_OD_API_IS_QUANTIZED = false;
    private static final String TF_OD_API_MODEL_FILE = "yolov4-416.tflite";
    private static final String TF_OD_API_LABELS_FILE = "file:///android_asset/coco.txt";
    private static final DetectorMode MODE = DetectorMode.TF_OD_API;
    private static final float MINIMUM_CONFIDENCE_TF_OD_API = 0.1f;
    private static final boolean MAINTAIN_ASPECT = false;
    private static final Size DESIRED_PREVIEW_SIZE = new Size(640, 480);
    private static final boolean SAVE_PREVIEW_BITMAP = false;
    private static final float TEXT_SIZE_DIP = 10;
```

In the file `\android\app\src\main\java\org\tensorflow\lite\examples\detection\MainActivity.java`, Adapt these lines to your needs.

```
    public static final float MINIMUM_CONFIDENCE_TF_OD_API = 0.4f;
    public static final int TF_OD_API_INPUT_SIZE = 416;
    private static final boolean TF_OD_API_IS_QUANTIZED = false;
    private static final String TF_OD_API_MODEL_FILE = "yolov4-416.tflite";
    private static final String TF_OD_API_LABELS_FILE = "file:///android_asset/coco.txt";
```

Adapt this code according to the number of classes you have in the same file. For example we have two classes.

```
    if (location != null && result.getConfidence() >= MINIMUM_CONFIDENCE_TF_OD_API) {
        if (result.getDetectedClass() == 0) {
            paint.setColor(Color.RED);
            textPaint.setColor(Color.RED);
        }else{
             paint.setColor(Color.GREEN);
             textPaint.setColor(Color.GREEN);
        }
        canvas.drawText(result.getConfidence().toString(), location.left,location.top,textPaint);
        canvas.drawRect(location, paint);
     }
```

### Use the app

Enjoy your app, you can use Android Studio for test it. To select images just touch the image.

Examples of predictions with images:

<div align="center"><img src="/elementsReadme/huevo.jpg" />
</div>

<div align="center"><img src="/elementsReadme/larva.jpg" />
</div>

<div align="center"><img src="/elementsReadme/larva2.jpg" />
</div>

Examples of predictions with camera:

<div align="center"><img src="/elementsReadme/videoLarva.jpg" />
</div>

<div align="center"><img src="/elementsReadme/VideoLarva2.jpg" />
</div>
