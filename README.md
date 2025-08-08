# Object-Detection-using-YOLOv8-
This GitHub repository consists of my projects done using Yolo for IIIT internship.
Task 1- OVERVIEW
For GNU/Linux box:

Create virtual environment https://docs.python.org/3/library/venv.html,
$ source /path/to/venv/bin/activate,
Ensure you are inside your virtual environment.. before proceeding,
Install ultralytics - follow steps given at https://docs.ultralytics.com/quickstart/,
Test installation with the example given, and verify whether the trained model can recognise objects and also perform segmentation from the online image.
BASICALLY,

the task is to set up a virtual environment in python. we then need to activate it.
Next, we need to install the yolov8 package by ultralytics, and then we have to perform a simple segmentation task on an online image.
Here are the steps i followed to complete the task-
Step 1: Python Installation
I installed Python version 3.13.3 from the official website.

Step 2: Created a Virtual Environment
I set up a virtual environment named "venv" in Visual Studio Code to manage dependencies. This was done using:
python -m venv venv

I activated it with:
venv\Scripts\activate


Step 3: Installed  Required Libraries
I installed the ultralytics library with the command:
pip install ultralytics


Step 4: Writing Python Code for Prediction
I wrote a Python script to perform image predictions using YOLOv8n. The script loads the model and runs predictions on an image as follows:
from ultralytics import YOLO
import matplotlib.pyplot as plt
import cv2
from PIL import Image, ImageDraw, ImageFont

model = YOLO("yolov8n.pt")
results = model("bus.jpg")
num_predictions = len(results[0].boxes)
img_pil = Image.open("bus.jpg")
draw = ImageDraw.Draw(img_pil)
for i, box in enumerate(results[0].boxes.xyxy):
    conf = results[0].boxes.conf[i] * 100
    x1, y1, x2, y2 = box.tolist()
    text = f"{conf:.2f}%"
    font = ImageFont.load_default()
    text_width, text_height = font.getbbox(text)[2:]
    bg_x1, bg_y1, bg_x2, bg_y2 = x1, y1 - text_height - 5, x1 + text_width + 5, y1
    draw.rectangle([bg_x1, bg_y1, bg_x2, bg_y2], fill="black")
    draw.text((x1 + 2, y1 - text_height - 3), text, fill="white", font=font)
    draw.rectangle(box.tolist(), outline="yellow", width=3)
img_pil.save("Final.jpg")


These steps outline my approach to achieving image predictions using YOLOv8n. 

