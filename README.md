# Tool-Detector

A classification model that classifies tools using resnet-18

![Tools](https://hips.hearstapps.com/hmg-prod/images/close-up-of-tools-hanging-on-wall-royalty-free-image-760251967-1563391812.jpg)

## The Algorithm

The Algorithm this project runs on uses Ai to recognize images. Using specific details obtained through hours of training, the computer is able to narrow down what kind of tool or item it is looking at.

## Running this project

1. Open VS Code and connect to your Jetson Nano.
2. Make sure you have installed Jetson Inference and Docker Image from : https://github.com/dusty-nv/jetson-inference/blob/master/docks/building-repo-2.md
3. Download the file and drag it into your library on the device where you're running the program. Make sure its located in the jetson-inference/python/training/classification/data
4. "cd" to nvidia/jetson-inference/.
5. Once it has run and you're back in the jetson-inference folder, run "./docker/run.sh" to run the docker container. You may need to re-enter your nvidia password at this step.
6. From inside the Docker container, change directories so you are in "jetson-inference/python/training/classification".
7. Run the scripts.

- Run the training script to re-train the network where the model-dir argument is where the model should be saved and where the data is. python3 train.py --model-dir=models/Tools data/Tools

    You should immediately start to see output, but it will take a very long time to finish running. It could take hours depending on how many epochs you run for your model.

    When running the model you can also specify the value of how many epochs and batch sizes you want to run. For example at the end of that code you can add: --batch-size=NumberOfBatchFiles --    workers=NumberOfWorkers --epochs=NumberOfEpochs

8. While it's running, you can stop it at any time using Ctl+C. You can also restart the training again later using the --resume and --epoch-start flags, so you don't need to wait for training to complete before testing out the model.

9. Make sure you are in the docker container and in jetson-inference/python/training/classification.
    
10. Run the onnx export script. python3 onnx_export.py --model-dir=models/Tools
    
11. Look in the jetson-inference/python/training/classification/models/Tools folder to see if there is a new model called resnet18.onnx there. That is your re-trained model.

12. Exit the docker container by pressing Ctl + D.

13. On your nano, navigate to the jetson-inference/python/training/classification directory.

14. Use ls models/Tools/ to make sure that the model is on the nano. You should see a file called resnet18.onnx.

15. Set the NET and DATASET variables NET=models/Tools DATASET=data/Tools

16. Run this command to see how it operates on an image from the test folder. imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/name/name.jpg TestImage1.jpg

[View a video explination here] (https://www.youtube.com/watch?v=l_iidyeYtJM)

Train.py here: 


