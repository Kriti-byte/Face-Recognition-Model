# Face-Recognition-Model
This is an implementation Facial Recognition using OpenCV implementation of Facenet and SVM

Setup before running the code:

Create dataset folder
Create sub-folders with names of the faces you want to recognize
In each sub-folder add the image of the person. There is no need to crop images. However, make sure that each image has only the pic of one person
Create a video folder
Add the video on which you want to run the algorithm on - preferably an mp4 video
Create an output folder. This will save the pickle files and the final output video.
Download the openface nn4.small2.v1.t7 model from the open face portal link (https://storage.cmusatyalab.org/openface-models/nn4.small2.v1.t7) You may also see the accuracy reports in the following link - http://cmusatyalab.github.io/openface/models-and-accuracies/
Make sure you have the relevant libraries of Opencv, imutils, pickle etc..
To run the code:

Extract the 128-D embeddings of the images in the dataset. This uses the Openface implementation of Facenet model. The embeddings are saved in the output folder "embeddings.pickle" file
==> python extract_embeddings.py --dataset dataset --embeddings output/embeddings.pickle --detector face_detection_model --embedding-model nn4.small2.v1.t7

Train the embeddings on a Support Vector Machine (SVM) classifier. This is used to detect different faces in the video. The SVM encodings are saved in "recognizer.pickle". The name encodings of the different faces you want to detect are stored in "le.pickle" file
==> python train_model.py --embeddings output/embeddings.pickle --recognizer output/recognizer.pickle --le output/le.pickle

Run the model on the video. The output video file can be mp4 or avi.
===> python recognize_video_file.py --detector face_detection_model --embedding-model nn4.small2.v1.t7 --recognizer output/recognizer.pickle --le output/le.pickle --input video/ --output output/
