Task -2 IIITH
Task Overview-
Image Segmentation: Write code to perform segmentation on a list of local images, extending the code for video processing after achieving segmented output for multiple images. Relevant code snippets can be found in Ultralytics documentation.
Video Retrieval: Obtain a video snippet from YouTube or another social media platform, ensuring the content is respectful.
Video to Image Conversion: Split the retrieved video into images at regular intervals using tools like FFmpeg.
Image to Video Conversion: After segmenting the extracted images, rejoin and convert them back into a new video, again using tools like FFmpeg if simpler options are unavailable.
What I understood about the task-
(a) Understanding YOLOv8 Segmentation

My first step was to understand how YOLOv8 handles segmentation — not just object detection — particularly when working with video. Segmentation involves identifying the exact pixels that belong to each object, which provides much finer detail than simply drawing bounding boxes.

I wrote a script that loads all images from a local folder, applies segmentation, and saves the results to a separate directory. The core method I used was model.predict(), where I passed the folder path instead of a single image. I had to ensure that all images were in the same format and located in the folder before executing the script.

(b) Downloading a Video-
I downloaded a video from youtube shorts- https://www.youtube.com/shorts/UxkH_Lj8whg

(c) Splitting the Video with FFmpeg

What is FFmpeg? It’s a powerful open-source command-line tool for processing video and audio. It supports tasks like format conversion, frame extraction, video creation from images, and more. Once installed and added to the system path, it can be run from any terminal.

To extract frames from the video, I used the following command:
ffmpeg -i downloaded.mp4 -vf fps=1 frames/frame_%04d.jpg
This command extracts one frame per second and names each frame sequentially. I created a frames folder in advance to keep everything organized.

(d) Segmenting Frames and Reconstructing the Video

After extracting the frames, I reused my segmentation script, this time pointing it to the frames/ directory. YOLOv8 segmented each frame and saved the results in the runs/segment/predict/ directory.

To turn the segmented images back into a video, I used another FFmpeg command:

ffmpeg -framerate 1 -i runs/segment/predict/image%04d.jpg -c:v libx264 -pix_fmt yuv420p output_video.mp4
This stitched the segmented images into a new video file.

Implementation of the task-
implementation part:
I extracted frames from the youtube video and saved them in the input file

segmentation on local images

from uitralytics import YOLO

import os

import cv2

model YOLO("yolov8x-seg.pt")

input folder = "local_images"

output folder = "segmented_images"

os.makedirs(output folder, exist_ok=True)

count = 1

for img in sorted(os.listdir(input_folder)):

if img.endswith((".jpg", ".jpeg", ".png")):

path = os.path.join(input_folder, img)

g)

results model.predict(source=path, save=False, stream=True)

for r in results:

seg_img = r.plot()

cv2.imwrite(os.path.join(output_folder, f" (count:04d}.jpg"), seg_im

print(f"Segmented (img)")

count += 1

extract frames from video using ffmpeg

mkdir frames

ffmpeg -i downloaded.mp4 -vf fps=1 frames/frame_%04d.jpg
( HAD TO SOME WORK LIKE SETTING THE FPS SETTING THE FRAME RATE AND RESOLUTION ETC)
FINALLY I SAVED THE OUTPUT VIDEO BY JOINNG ALL THE EXTRACTED FRAMES BACK AGAIN AS A NORMAL VIDEO(although the fps decreased a bit) BUT YAH THE PROCESS DID WORK AND WAS ABLE TO DETECT ' PLAYERS' AND 'BASKETBALL' AS AN 'OBJECT'.
