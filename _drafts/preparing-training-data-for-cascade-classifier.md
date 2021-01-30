---
title: Preparing Training Data for Cascade Classifier
date: 2021-01-30
categories: programming
---

I've been building a bot for a game called Audiosurf 2. In that game, you play as a ship that collects blocks and avoid spikes. I used OpenCV, a computer vision library, for processing the images. I followed a few tutorials on YouTube on training a Haar cascade classifier. The results were disappointing. I had a lot of false positives because I did not understand how to prepare samples for the model to train with.

<!--more-->

## Reading the Docs

For any programming problem, I first Googled the problem to see how other people solved it. I did not find a direct answer to my problem. OpenCV is a large library so there are many similar questions, but very different implementations. I spent the next couple hours turning all the links purple but did not find what I was looking for. The good thing is that a lot of people recommended the OpenCV documentations instead.

I always tend to avoid reading the docs because they either are lacking or not easy to understand. But I was pleasantly surprised when the docs on [cascade training](https://docs.opencv.org/3.4/dc/d88/tutorial_traincascade.html) was simple and straightforward.

## Negative Samples

The docs recommend the negative samples be taken from arbitrary images not containing what I wanted to detect. For example, if I wanted to detect a car, my negative samples would be anything that is not a car. The difficult part for me was that my images contain both negative and positive samples.

<p align="center">
  <img src="#" alt="Audiosurf 2 Image">
</p>

### Cropping Image Contours

A method I tried was cropping out the contours of the objects. I found a [method](https://www.quora.com/How-can-I-detect-an-object-from-static-image-and-crop-it-from-the-image-using-openCV) on Quora that did this for me:

```py
    import cv2  
    image = cv2.imread("example.jpg") 
    gray=cv2.cvtColor(image,cv2.COLOR_BGR2GRAY) 
    edged = cv2.Canny(image, 10, 250) 
    (cnts, _) = cv2.findContours(edged.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE) 
    idx = 0 
    for c in cnts: 
    	x,y,w,h = cv2.boundingRect(c) 
    	if w>50 and h>50: 
    		idx+=1 
    		new_img=image[y:y+h,x:x+w] 
    		cv2.imwrite(str(idx) + '.png', new_img) 
    cv2.imshow("im",image) 
    cv2.waitKey(0) 
```

It created a lot of fragments from my image due to unclear boundaries between objects. The cropped images also contained the blocks I want to detect in there. If I chose to use this method, I needed to go through all the cropped images and remove the positive samples. It was not a viable solution.

<p align="center">
  <img src="#" alt="Image Contours">
</p>

### Hiding Positive Samples

I went back to the docs and read it more carefully this time. The negative samples tell the model what not to look for. I thought about it and realized that my whole image is essentially a big negative sample. The only thing I want to detect is the block and nothing else. I need to hide the block in the image.

That simply meant I went and drew a black box to cover the block.

<p align="center">
  <img src="#" alt="Hiding Positive Sample in Image">
</p>

## Positive Samples

### Annotating Images

In [OpenCV 3.3.14](https://sourceforge.net/projects/opencvlibrary/files/3.4.13/), the extracted files included an annotation tool for drawing boxes around positive samples of an image. It generates a `txt` file containing the coordinates of the window I drew on the image. The command to run the tool:

```sh
opencv_annotation.exe --annotations=pos_block.txt --images=positive_block/
```

<p align="center">
  <img src="#" alt="Annotating Image">
</p>

The process was tedious when I had 350 images to go over. There are probably better ways but I wanted to see how good the model was before writing more code to automate it.

### Creating Vector File

After that was done, I ran another command for the `createsample` application:

```sh
opencv_createsamples.exe -info pos_block.txt -w 24 -h 24 -num 1200 -vec pos_block.vec
```

This application generated a positive sample dataset. It had two different ways to do this: artificially creating samples from one image or using all the manually created samples. The second way results in a more robust model. That's why I used the annotation tool earlier to highlight all the positive samples in the image.

## Training the Model

Training the model was straightforward. I ran the command:

```sh
opencv_traincascade.exe -data cascade_block/ -vec pos_block.vec -bg neg_block.txt -numPos 900 -numNeg 350 -numStages 25 -w 24 -h 24 -precalcValBufSize 2048 -precalcIdxBufSize 2048
```

It took me several training sessions to get what I wanted. Training a cascade can take a long time so I usually run it for 10 stages and test the result before more training.

Preparing good data is the most important process for machine learning. I used random images before and the result was bad. By taking my time to manually creating negative and positive samples, I ensured my model is effective.