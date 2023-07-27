Sponge 

This model is used to detect surgical sponges that are on a surgical tray. It is trained on an imagenet Resnet-18 model using transfer learning. The idea is that if it can detect where the sponges are, it will be easier to see and count them, which could potentially reduce the amount of Retained Surgical Items (gossypiboma) cases. 

## The Algorithm
The algorithim is used by taking a picture (format: PASCAL VOC) - supported by Jetson nano. It uses a 2GB Jetson Nano, and so it uses it a preflashed SD card flashed from the NVIDIA webpage. It uses a detectnet to detect the sponge, then it crops the image to just hold the face. It then sends the sponge to the transfer learning model. The transfer model then detects the sponge(s). 
Note: I ran this model on a realivly low epoch with information that was askew. The pretrained model is quite inacurrate.
## Running this project

1. Connect to your Jetson Nano via VSCODE. 
2. Insert the data set into VS Code (XML in Annotations, JPEG in JPEGImages). Create a file named 'ImageSets' with 4 .txt files: test.txt, train.txt, trainval.txt, val.txt. 
3. Ensure that you have the proper things installed. The Renet18.onnx and all others like that - the ones that say resnet18.onnx and the final_project.py. Also, ensure that you have the labels.txt file. 
4. Since using teh preflashed SD card, there sould be a docker container. This is accesable by implementing this code. Change directories into jetson-inference/python/training/detection/ssd
5. Then run this code python3 train_ssd.py --dataset-type=voc --data=data/<YOUR-DATASET> --model-dir=models/<YOUR-MODEL>. This will train the data. 
6a. After it's finished training, run python3 onnx_export.py --model-dir=models/<YOUR-MODEL> to export the model.
6b. To run the program, 
7. The model is up and running, and so you should just put your face in clear view infront of the camera and watch as it tries to predict your age!

[View a video explanation here](video link)
