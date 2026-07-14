# Posture Detector
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Tanvi T | Millburn High School | Electrical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



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
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Raspberry Pi 4 Kit | Raspberry Pi to run pose estimation | $147.69 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/dp/B0C8LV6VNZ?tag=mh0b-20&ref=pd_sl_2z1ubaby08_e&msclkid=01f71c5c545615ea9a6a760a61f934fc&th=1)"> Link </a> |
| Raspberry Pi Camera | Camera to capture live feed | $10 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/Arducam-Raspberry-Camera-Module-1080P/dp/B07RWCGX5K/ref=asc_df_B07RWCGX5K?tag=bingshoppinga-20&linkCode=df0&hvadid=79989681303579&hvnetw=o&hvqmt=e&hvbmt=be&hvdev=c&hvlocint=&hvlocphy=58299&hvtargid=pla-4583589158924862&hvocijid=7734632799255230196-B07RWCGX5K-&hvexpln=0&th=1)"> Link </a> |
| Electronics Kit | Circuit components | $11.98 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/ELEGOO-Electronics-Potentiometer-tie-Points-Breadboard/dp/B09YRJQRFF)"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
