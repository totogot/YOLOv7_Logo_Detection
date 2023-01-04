# Logo Detection using YOLOv7

Repository showing an example of how to train a YOLOv7 model to detect logo detection in images. The main.ipynb contains the run code, with accompanying commentary.

This project makes use of the YOLO model architecture (using Wong Kin Yiu's YOLOv7 repo: https://github.com/WongKinYiu/yolov7'). While this repor provides commentary and examples, for full YOLO documentation, I recommend viewing WongKinYiu's GitHub.

The model is custom trained using a manually tagged dataset of images featuring the Petronas company logo, before using the model to infer the presence of the logo in a video of Formula 1 racing. The intention is to see how often the logo appears in the frames, and how much screen space the logo takes up.


## Initial setup
The first thing you are going to want to do is to clone this repository. To do this, you can use CLI to do the following:
```
$ cd C:\Users\jdoe\Documents\PersonalProjects
$ git clone https://github.com/totogot/YOLOv7_Logo_Detection.git
```

Next set up a virtual environment for installing all package requirements into
```
$ cd C:\Users\jdoe\Documents\PersonalProjects\YOLOv7_Logo_Detection
$ python -m venv venv
```

Then from within the terminal command line within your IDE (making sure you are in the project folder), you can install all the dependencies for the project, by simply activating the venv and leveraging the setuptools package and the setup.cfg file created in the project repo. 

Note: for IDEs where the CLI uses PowerShell by default (e.g. VS Code), in order to run Activate.ps1 you may find that you first need to update your settings such that Command Prompt is the default terminal shell - see here: https://support.enthought.com/hc/en-us/articles/360058403072-Windows-error-activate-ps1-cannot-be-loaded-because-running-scripts-is-disabled-UnauthorizedAccess-

```
$ .\venv\Scripts\activate
$ pip install --upgrade pip
$ pip install .
```

This last command will install all dependencies outlined in the setup.cfg file. 
Note: ipykernel has been included to enable the main.ipynb to be run also and for relevant visualisations to be outputted also.


## Running model training and inference
All workings and accompanying commentary around custom training and then subsequent inference can be found in the "main.ipynb" file. 

Note: the final model weights have not been saved as part of this GitHub repo due to limited storage


## Cloning official YOLOv7 repository
The official YOLOv7 repo by Wong Kin Yiu (https://github.com/WongKinYiu/yolov7) has been cloned into this project (folder "yolov7") in order to provide a clear repeatable example of my project repository. However, for full details on usage and licensing I recommend looking at the repo yourself. Additionally, I do not claim any credit for the material that sits within this folder.

Further to avoid duplication of repositories, if you are following along with the guidance in this projects "main.ipynb", I recommend first deleting the yolov7 repo folder, to avoid duplication


## Image data 

This project was built using a custom made dataset with 100 images containing the Petronas company logo, with fine-grained (annotated, including bounding boxes) labelled data obtained through manual tagging myself. 

It is worth noting that this volume of data is unlikely to lead to a high degree of accuracy, and in the real world you would anticipate providing a far larged dataset during training in order to develop a robust and accurate model for deployment - i.e. >1500 images per class. However, for the purpose of showing an end to end project, and to reduce the time and compuational power required for training, I deemed 100 images as sufficient.


## Labelling data

To label the images myself, I decided to utilise LabelStudio (https://labelstud.io/), as it is a free open-source VoTT (Viual Object Tagging Tool), with simple download.

To get started simply open up a terminal (in my case I use Windows Command Prompt), and execute the following commands:
```
$ pip install label-studio
$ label-studio start
```

This will install the LabelStudio requirements and then launch the programme in a new browser window. From there you should set up your tagging task, following the instructions found here (https://labelstud.io/guide/index.html#Quick-start). Once you have completed your tagging task, you can export the annotated dataset (in one of many different formats). 

For the purpose of this project, and to ensure that only one single annotation file is created, I opted for the COCO JSON format