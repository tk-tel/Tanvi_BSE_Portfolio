
# Posture Detector

Bad posture is something that a lot of people struggle with, especially as we spend more and more time on our computers and phones. To tackle this issue and fix my own bad posture, I designed a posture detector that runs on a raspberry pi and processes a live camera feed to detect if the user has bad posture. An LED visually shows posture status and a buzzer goes off when the user needs to fix their posture. I faced many challenges in set-up, getting the code to work, and integrating circuit components, but I am very proud of the final product. I plan to add more features to make this a device I can use in my daily life.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Tanvi T | Millburn High School | Electrical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image]<img width="3055" height="2796" alt="IMG_2860" src="https://github.com/user-attachments/assets/50827f45-5f06-47ff-bab6-75e9c198e95a" />
  
# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/d8hTNZIYgD8?si=CP_50_oF4deXSfz9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

For my third milestone, I added modifications to my code and I added circuit components. 

In my original code, it would output bad posture even if my posture was perfect but I was looking down. I tried finding a way to calculate posture that wasn’t determined by head coordinates but since the head is a huge part of posture, I ultimately decided to add another “mode” to my code. I called this papermode for tasks done on paper and not on the computer. The user enters this mode when they have a specific nose to shoulder angle and while in this mode, the threshold for bad posture is different.

Another problem I had with the original code is that every time I tested it, the threshold would be different. I realized that even though I was calculating the angle instead of distance, due to posenet outputting 2D coordinates instead of 3D, it would change based on the position of the camera. So, I added calibration to my code. Right after turning on the device, it asks for an example of good and bad posture and calculates a threshold in between. 

The second half of my modifications was adding circuit components, specifically an LED and buzzer. I started with just turning on a red LED but switched to an RGB LED because I wanted to differentiate between all the possible postures. I also added a passive buzzer, but the GPIO pins weren’t supplying enough current so I added a transistor to safely increase the amount of current supplied.

After finishing all the code and wiring, the main issue that remained was that the detection was jittery and the LED was flickering between colors. I realized that it was because it was outputting every instance of bad posture even if it was just a glitch, so I added a moving average to make sure it ignored random extreme values.

My project still needs some edits to improve accuracy but overall, it is complete. Through this project, I learned how to set-up and code on a raspberry pi, how to use a ML model to process images from a live camera feed, how to wire circuit components, and most importantly, how to troubleshoot and persevere. 

For further steps, I plan on 3D printing a case to hold the camera in place and designing a custom PCB so I can make it a proper device that I can use in my daily life. I also aim to make more projects that build on what I have learned.





# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/uOBhi_VRXXk?si=AUENxLJLNYaVc7p8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


My second milestone includes finishing my base project, which is pose estimation, and adding the functionality for a specific use case, which is posture detection. Even though I was originally planning on using pose estimation to do fall detection, I pivoted to posture detection. This is because I wouldn’t really have been able to implement fall detection in any useful way with what I had. The camera was too narrow, the fps too low for me, and actual fall detection devices have many more computationally heavy features to maximize safety. Given the resources I had, I decided to do posture detection instead, which is a problem I personally have and can realistically fix with my current prototype.

Pose estimation:
Pose estimation models use a Convolutional Neural Network (CNN) to process input images and output the coordinates of keypoints corresponding to various body parts. Originally, I tried using mediapipe instead of posenet for the model because it is more accurate, has better performance, and is easier to implement. However, there were many errors, such as picamera2 not working, opencv not working, and more. I realized that mediapipe was not compatible with python v3.13 so I tried to install an older version manually but the code didn’t work with all the packages having different versions. I switched to posenet which is part of tensorflow and works with the latest version of python. Posenet uses a CNN to output a heatmap and an offset map, which coordinates must then be calculated from to do pose estimation.

Posture detection:
At first, I calculated bad posture based on the distance between two coordinates but this wasn’t accurate because it would change if I moved closer or further from the camera. I decided to fix this by calculating the angle between the ear and shoulder instead. I printed the angle to the terminal and sat in different postures to find a threshold value I could use to detect bad posture. If the angle exceeds that, it prints bad posture to the terminal.

I also tried other methods of calculating bad posture, like the ratio of the neck to shoulder distance to shoulder to shoulder distance, but ultimately the first way worked the best.

Now that the base project is done, I plan on incorporating LEDs and a buzzer warning to visually and audibly alert the user if they have bad posture.
 

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/bkzAmk7Hbp8?si=3LKAEFJw7jNDCuPX" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The core functionality of my project is pose estimation. While my milestone video describes its application as fall detection, I have since modified it to be a pose detector to prevent strain and headaches.

My first milestone for this project consisted of two main components: setting up the hardware and making sure the camera worked properly.

For the first part, the physical setup began by flashing the Raspberry Pi OS onto a microSD card. After flashing the OS onto the pi, my goal was to run it 'headless,' meaning without a monitor, keyboard, or mouse attached to the Pi itself. To achieve this, I set up RealVNC viewer so I could view the Pi's desktop remotely, and I configured SSH to securely access the command line terminal from my main computer.

During this setup stage, I had many challenges, particularly with the VNC connection. Initially, my connection kept timing out entirely. I had to troubleshoot by using the command sudo raspi-config to manually turn the remote desktop interface permissions on. After I solved that, there was another challenge: the VNC screen was completely blank and gray. Because the Pi didn't detect a physical monitor plugged into its HDMI port, it refused to draw a desktop. I fixed this by going back into the configuration settings and forcing a specific display resolution.

For the second part of my milestone, I set up the camera module. I connected it to the raspberry pi and I started with simple terminal tests using the rpicam-still command. From there, I used Picamera2 – a python library specifically designed for the pi camera module – to take videos.

The main challenge during this stage was that after setting up the camera, my SSH access stopped working entirely. After a bit of confusion, I realized that while I was trying to fix my camera permissions, I had accidentally disabled SSH. Because I was completely locked out, I had to connect the Pi directly to a monitor, plug in a temporary keyboard, and manually re-enable SSH. 

After completing this set-up, the goal for the next milestone is to get the pose estimation model to output coordinates for 17 points on the body.


# Schematics 

<img width="637" height="372" alt="Screenshot 2026-07-14 101842" src="https://github.com/user-attachments/assets/f35a6830-87cd-4d56-a191-5c8feece4b38" />


# Code

```python
import os
import cv2
import numpy as np
import math
import tensorflow as tf
import time
from threading import Thread, Lock
from picamera2 import Picamera2
import RPi.GPIO as GPIO

class VideoStream:
    def __init__(self, resolution=(640, 480)):
        self.stream = Picamera2()
        config = self.stream.create_video_configuration(
            main={"format": "BGR888", "size": resolution}
        )
        self.stream.configure(config)
        self.stream.start()
        print("Pi Camera (libcamera/picamera2) initiated successfully.")

        self.frame = self.stream.capture_array()
        self.grabbed = self.frame is not None

        self.stopped = False

    def start(self):
        Thread(target=self.update, args=()).start()
        return self

    def update(self):
        while True:
            if self.stopped:
                self.stream.stop()
                return
            self.frame = self.stream.capture_array()
            self.grabbed = True

    def read(self):
        return self.frame

    def stop(self):
        self.stopped = True


MODEL_PATH = "posenet_mobilenet_v1_100_257x257_multi_kpt_stripped.tflite"
min_conf_threshold = 0.5
imW, imH = 1280, 720
output_stride = 32

PART_INDEX = {
    "nose": 0, "leftEye": 1, "rightEye": 2, "leftEar": 3, "rightEar": 4,
    "leftShoulder": 5, "rightShoulder": 6, "leftElbow": 7, "rightElbow": 8,
    "leftWrist": 9, "rightWrist": 10, "leftHip": 11, "rightHip": 12,
    "leftKnee": 13, "rightKnee": 14, "leftAnkle": 15, "rightAnkle": 16,
}

interpreter = tf.lite.Interpreter(model_path=MODEL_PATH)
interpreter.allocate_tensors()

input_details = interpreter.get_input_details()
output_details = interpreter.get_output_details()
height = input_details[0]['shape'][1]
width = input_details[0]['shape'][2]

floating_model = (input_details[0]['dtype'] == np.float32)
input_mean = 127.5
input_std = 127.5

def mod(a, b):
    floored = np.floor_divide(a, b)
    return np.subtract(a, np.multiply(floored, b))

def sigmoid(x):
    return 1 / (1 + np.exp(-x))

def sigmoid_and_argmax2d(threshold):
    v1 = interpreter.get_tensor(output_details[0]['index'])[0]
    h_shape, w_shape, depth = v1.shape
    reshaped = np.reshape(v1, [h_shape * w_shape, depth])
    reshaped = sigmoid(reshaped)
    reshaped = (reshaped > threshold) * reshaped
    coords = np.argmax(reshaped, axis=0)
    yCoords = np.round(np.expand_dims(np.divide(coords, w_shape), 1))
    xCoords = np.expand_dims(mod(coords, w_shape), 1)
    return np.concatenate([yCoords, xCoords], 1)

def get_offset_point(y, x, offsets, keypoint, num_key_points):
    y_off = offsets[y, x, keypoint]
    x_off = offsets[y, x, keypoint + num_key_points]
    return np.array([y_off, x_off])

def get_offsets(coords, num_key_points=17):
    offsets = interpreter.get_tensor(output_details[1]['index'])[0]
    offset_vectors = np.array([]).reshape(-1, 2)
    for i in range(len(coords)):
        heatmap_y = int(coords[i][0])
        heatmap_x = int(coords[i][1])
        if heatmap_y > 8: heatmap_y = heatmap_y - 1
        if heatmap_x > 8: heatmap_x = heatmap_x - 1
        offset_vectors = np.vstack((offset_vectors, get_offset_point(heatmap_y, heatmap_x, offsets, i, num_key_points)))
    return offset_vectors

def get_part_yx(keypoint_positions, drop_pts, part_name):
    idx = PART_INDEX[part_name]
    if idx in drop_pts:
        return None, None
    return keypoint_positions[idx][0], keypoint_positions[idx][1]

def get_angle(x1, y1, x2, y2):
    delta_x = abs(x1 - x2)
    delta_y = abs(y1 - y2)
    angle_rad = math.atan2(delta_x, delta_y)
    angle_deg = math.degrees(angle_rad)
    return angle_deg

videostream = None

GPIO.setmode(GPIO.BCM)
redpin = 12
greenpin = 19
bluepin = 13
GPIO.setup(redpin, GPIO.OUT)
GPIO.setup(greenpin, GPIO.OUT)
GPIO.setup(bluepin, GPIO.OUT)

buzzerpin = 17
frequency = 261.63
GPIO.setup(buzzerpin, GPIO.OUT)
pwm = GPIO.PWM(buzzerpin, frequency) 

def alert():  
    pwm.start(10)

def stop_alert():
    pwm.stop()

buzzer_on = False

def start_buzzer():
    global buzzer_on
    if not buzzer_on:
        alert()
        buzzer_on = True

def stop_buzzer():
    global buzzer_on
    if buzzer_on:
        stop_alert()
        buzzer_on = False

def off():
    GPIO.output(redpin, GPIO.LOW)
    GPIO.output(greenpin,GPIO.LOW)
    GPIO.output(bluepin,GPIO.LOW)

def green():
    GPIO.output(redpin, GPIO.LOW)
    GPIO.output(greenpin,GPIO.HIGH)
    GPIO.output(bluepin,GPIO.LOW)
    stop_buzzer()

def red():
    GPIO.output(redpin, GPIO.HIGH)
    GPIO.output(greenpin,GPIO.LOW)
    GPIO.output(bluepin,GPIO.LOW)
    start_buzzer()

def yellow():
    GPIO.output(redpin, GPIO.HIGH)
    GPIO.output(greenpin,GPIO.HIGH)
    GPIO.output(bluepin,GPIO.LOW)

def blue():
    GPIO.output(redpin, GPIO.LOW)
    GPIO.output(greenpin,GPIO.LOW)
    GPIO.output(bluepin,GPIO.HIGH)
    stop_buzzer()

def purple():
    GPIO.output(redpin, GPIO.HIGH)
    GPIO.output(greenpin, GPIO.LOW)
    GPIO.output(bluepin, GPIO.HIGH)

def blink(color):
    for _ in range(3):
        color()
        time.sleep(0.5)
        off()
        time.sleep(0.5)

def get_angle_samples(get_angle_fn):
    samples = []
    start = time.time()
    while time.time() - start < 3:
        angle = get_angle_fn()
        if angle is not None:
            samples.append(angle)
        time.sleep(0.05)
    return sum(samples) / len(samples) if samples else None

def get_keypoints_droppts():
    frame1 = videostream.read()

    if frame1 is None:
        time.sleep(0.01)
        return None, []

    frame = frame1.copy()
    frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    frame_resized = cv2.resize(frame_rgb, (width, height))
    input_data = np.expand_dims(frame_resized, axis=0)

    if floating_model:
        input_data = (np.float32(input_data) - input_mean) / input_std

    interpreter.set_tensor(input_details[0]['index'], input_data)
    interpreter.invoke()

    coords = sigmoid_and_argmax2d(min_conf_threshold)
    drop_pts = list(np.unique(np.where(coords == 0)[0]))
    offset_vectors = get_offsets(coords)
    keypoint_positions = coords * output_stride + offset_vectors
    return keypoint_positions, drop_pts

def get_current_normal_angle():
    result = get_keypoints_droppts()
    if result[0] is None:
        return None
    keypoint_positions, drop_pts = result
    ey, ex = get_part_yx(keypoint_positions, drop_pts, "leftEar")
    sy, sx = get_part_yx(keypoint_positions, drop_pts, "leftShoulder")
    if ex is None or sx is None:
        return None
    return get_angle(ex, ey, sx, sy)

def run_calibration():
    print("=== Calibration starting ===")

    blink(green)
    print("Hold GOOD posture...")
    good_normal = get_angle_samples(get_current_normal_angle)
    if good_normal is None: good_normal = 20.0
    print(f"Good posture angle: {good_normal:.1f}")

    blink(yellow)
    print("Hold BAD posture...")
    bad_normal = get_angle_samples(get_current_normal_angle)
    if bad_normal is None: bad_normal = 25.0
    print(f"Bad posture angle: {bad_normal:.1f}")

    blink(blue)
    print("Hold GOOD paper-mode posture...")
    good_paper = get_angle_samples(get_current_normal_angle)
    if good_paper is None: good_paper = 30.0
    print(f"Good paper angle: {good_paper:.1f}")

    blink(purple)
    print("Hold BAD paper-mode posture...")
    bad_paper = get_angle_samples(get_current_normal_angle)
    if bad_paper is None: bad_paper = 40.0
    print(f"Bad paper angle: {bad_paper:.1f}")

    posture_threshold = (good_normal + bad_normal) / 2
    paper_threshold = (good_paper + bad_paper) / 2

    print(f"=== Calibration done. Thresholds: normal={posture_threshold:.1f}, paper={paper_threshold:.1f} ===")
    return posture_threshold, paper_threshold

def process_loop(posture_threshold, paper_threshold):
    global output_frame
   
    recent_angles = []
    recent_paper_angles = []
    MOVING_AVERAGE_WINDOW = 5
    recent_head_angles = []
    HEAD_MOVING_AVERAGE_WINDOW = 5

    normal_slouch_start_time = None
    paper_slouch_start_time = None
    POSTURE_TIME_THRESHOLD = 5
    
    POSTURE_ANGLE_THRESHOLD = posture_threshold 
    PAPER_ANGLE_THRESHOLD = paper_threshold 
    BEND_THRESHOLD = 65
    papermode = False
    off()   
    
    while True:
        frame1 = videostream.read()

        if frame1 is None:
            time.sleep(0.01)
            continue

        frame = frame1.copy()
        frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
        frame_resized = cv2.resize(frame_rgb, (width, height))
        input_data = np.expand_dims(frame_resized, axis=0)

        if floating_model:
            input_data = (np.float32(input_data) - input_mean) / input_std

        interpreter.set_tensor(input_details[0]['index'], input_data)
        interpreter.invoke()

        coords = sigmoid_and_argmax2d(min_conf_threshold)
        drop_pts = list(np.unique(np.where(coords == 0)[0]))
        offset_vectors = get_offsets(coords)
        keypoint_positions = coords * output_stride + offset_vectors

        eary, earx = get_part_yx(keypoint_positions, drop_pts, "leftEar")
        shouldery, shoulderx = get_part_yx(keypoint_positions, drop_pts, "leftShoulder")
        nosey, nosex = get_part_yx(keypoint_positions, drop_pts, "nose")

        if nosex is not None and nosey is not None and earx is not None and eary is not None:
            head_angle = get_angle(nosex, nosey, earx, eary)
            recent_head_angles.append(head_angle)
            if len(recent_head_angles) > HEAD_MOVING_AVERAGE_WINDOW:
                recent_head_angles.pop(0)
            smoothed_head_angle = sum(recent_head_angles) / len(recent_head_angles)
            newpapermode = smoothed_head_angle <= BEND_THRESHOLD
            if newpapermode is not papermode:
                normal_slouch_start_time = None
                paper_slouch_start_time = None
                recent_angles.clear()
                recent_paper_angles.clear()
            papermode = newpapermode
    
        if earx is not None and shoulderx is not None and eary is not None and shouldery is not None and papermode is False:
            angle = get_angle(earx,eary,shoulderx,shouldery)
        
            recent_angles.append(angle)

            if len(recent_angles) > MOVING_AVERAGE_WINDOW:
                recent_angles.pop(0)

            smoothed_angle = sum(recent_angles) / len(recent_angles)

            if smoothed_angle > POSTURE_ANGLE_THRESHOLD:
                if normal_slouch_start_time is None:
                    normal_slouch_start_time = time.time()
                else:
                    elapsed_slouch_time = time.time() - normal_slouch_start_time
                    yellow()
                    if elapsed_slouch_time >= POSTURE_TIME_THRESHOLD:
                        red()
            else:
                if normal_slouch_start_time is not None:
                    normal_slouch_start_time = None
                green()
        
        elif earx is not None and shoulderx is not None and eary is not None and shouldery is not None and papermode is True: 
            if normal_slouch_start_time is not None:
                normal_slouch_start_time = None
            paper_angle = get_angle(earx,eary,shoulderx,shouldery)
            recent_paper_angles.append(paper_angle)

            if len(recent_paper_angles) > MOVING_AVERAGE_WINDOW:
                recent_paper_angles.pop(0)

            smoothed_angle = sum(recent_paper_angles) / len(recent_paper_angles)

            if smoothed_angle > PAPER_ANGLE_THRESHOLD:
                if paper_slouch_start_time is None:
                    paper_slouch_start_time = time.time()
                else:
                    elapsed_slouch_time = time.time() - paper_slouch_start_time
                    purple()
                    if elapsed_slouch_time >= POSTURE_TIME_THRESHOLD:
                        red()
            else:
                if paper_slouch_start_time is not None:
                    paper_slouch_start_time = None
                blue()    

if __name__ == "__main__":
    videostream = VideoStream(resolution=(imW, imH)).start()
    time.sleep(2.0)
    
    calibrated_posture, calibrated_paper = run_calibration()
    
    print("Posture monitoring system active. Press Ctrl+C to stop.")
    
    try:
        process_loop(calibrated_posture, calibrated_paper)
        
    except KeyboardInterrupt:
        print('\nInterrupted via terminal.')
        
    finally:
        if videostream is not None:
            videostream.stop()
        GPIO.cleanup()
        print('Resources safely terminated.')
```

# Bill of Materials 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Raspberry Pi 4 Kit | Raspberry Pi to run pose estimation | $147.69 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/dp/B0C8LV6VNZ?tag=mh0b-20&ref=pd_sl_2z1ubaby08_e&msclkid=01f71c5c545615ea9a6a760a61f934fc&th=1)"> Link </a> |
| Raspberry Pi Camera | Camera to capture live feed | $10 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/Arducam-Raspberry-Camera-Module-1080P/dp/B07RWCGX5K/ref=asc_df_B07RWCGX5K?tag=bingshoppinga-20&linkCode=df0&hvadid=79989681303579&hvnetw=o&hvqmt=e&hvbmt=be&hvdev=c&hvlocint=&hvlocphy=58299&hvtargid=pla-4583589158924862&hvocijid=7734632799255230196-B07RWCGX5K-&hvexpln=0&th=1)"> Link </a> |
| Electronics Kit | Circuit components | $11.98 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/ELEGOO-Electronics-Potentiometer-tie-Points-Breadboard/dp/B09YRJQRFF)"> Link </a> |

# Sources

- https://medium.com/analytics-vidhya/pose-estimation-on-the-raspberry-pi-4-83a02164eb8e
- https://www.instructables.com/Raspberry-Pi-Tutorial-How-to-Use-a-RGB-LED/ 
