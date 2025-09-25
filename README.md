
Aim:
 
To write a python program using OpenCV to capture the image from the web camera and do the following image manipulations.
i) Write the frame as JPG 
ii) Display the video 
iii) Display the video by resizing the window
iv) Rotate and display the video

## Software Used
Anaconda - Python 3.7
## Algorithm
### Step 1:
Use cv2.VideoCapture(0) to access web camera
### Step 2:
Use cv2.imread to read the video or image

### Step 3:
Use cv2.imwrite to save the image

### Step 4:
Use cv2.imshow to show the video

### Step 5:
End the program and close the output video window by pressing 'q'.

## Program:
``` Python
### Developed By:Ramya.P
### Register No:212223240137

from IPython.display import display, Javascript
from google.colab.output import eval_js
from base64 import b64decode
import cv2
import numpy as np
from google.colab.patches import cv2_imshow

def capture_frame():
    js = Javascript('''
    async function takePhoto() {
      const div = document.createElement('div');
      const video = document.createElement('video');
      div.appendChild(video);
      document.body.appendChild(div);
      const stream = await navigator.mediaDevices.getUserMedia({video: true});
      video.srcObject = stream;
      await video.play();
      const canvas = document.createElement('canvas');
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      canvas.getContext('2d').drawImage(video, 0, 0);
      stream.getTracks().forEach(track => track.stop());
      div.remove();
      return canvas.toDataURL('/content/Screenshot 2025-09-22 215135.png', 1.0);
    }
    ''')
    display(js)
    data = eval_js('takePhoto()')
    binary = b64decode(data.split(',')[1])
    nparr = np.frombuffer(binary, np.uint8)
    frame = cv2.imdecode(nparr, cv2.IMREAD_COLOR)
    return frame

## i) Write the frame as JPG file
frame = capture_frame()
cv2.imwrite("/content/Screenshot 2025-09-22 215135.png", frame)
print("Image saved as captured_image.jpg")
cv2_imshow(frame)



## ii) Display the video
frame = capture_frame()
cv2_imshow(frame)



## iii) Display the video by resizing the window

frame = capture_frame()
height, width, _ = frame.shape
smaller_frame = cv2.resize(frame, (0,0), fx=0.5, fy=0.5)
image = np.zeros_like(frame)
image[:height//2, :width//2] = smaller_frame
cv2_imshow(image)


## iv) Rotate and display the video

frame = capture_frame()
rotated = cv2.rotate(frame, cv2.ROTATE_90_CLOCKWISE)
cv2_imshow(rotated)







```
## Output

### i) Write the frame as JPG image
<img width="606" height="445" alt="image" src="https://github.com/user-attachments/assets/8988d139-7d13-4388-a8f0-48204c58e192" />



### ii) Display the video
<img width="597" height="443" alt="image" src="https://github.com/user-attachments/assets/cd1ec9a7-b3b1-4b45-908d-9fbe98c93bfe" />



### iii) Display the video by resizing the window
<img width="605" height="445" alt="image" src="https://github.com/user-attachments/assets/3a50a09c-3c23-4c34-bdf8-9f399f9c085d" />



### iv) Rotate and display the video
<img width="450" height="597" alt="image" src="https://github.com/user-attachments/assets/0d307b55-bd66-45ce-8cd2-1fc641aa4717" />




## Result:
Thus the image is accessed from webcamera and displayed using openCV.
