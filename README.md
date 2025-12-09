# Smart Traffic Light Optimization System (YOLO + Fuzzy Logic + IoT)
This project is a traffic light optimization system based on vehicle detection, PCU calculation, and automatic signal duration adjustment using Fuzzy Logic. This system combines a computer vision model, cloud server, and IoT microcontroller to produce adaptive and real-time traffic light settings.

Project Objectives : 
- Create an artificial intelligence-based adaptive traffic light system simulation
- Reduce traffic congestion using PCU calculations and fuzzy logic
- Integrate AI, cloud computing, and IoT models into one complete system
- Compare the performance of various detection models (YOLO vs RT-DETR vs FCOS)

System Integration Flow :
- The system starts by opening an AWS EC2 server (Ubuntu Linux) as the model deployment location. This server handles image analysis using a hosted vehicle detection model
- User are asked to enter traffic condition images and select a detection model (YOLOv11, RT-DETR, FCOS, etc.), after which the images will be processed and detection results will be generated
- From the detection results, the system converts the number of vehicles into PCU (Passenger Car Unit) to measure the density level of each direction of the intersection. The PCU is then used to calculate the recommended duration of green and red lights for each direction based on a fuzzy logic algorithm, with an additional ±12 seconds adjustment due to the interval: Red → Yellow: ~1.5 seconds, Green → Red: ~1 second
- The Raspberry Pi Pico + ESP-01S WiFi initially uses the default duration: Green: 10 seconds and Red: 42 seconds.
However, after AWS generates a new duration, the Pico will retrieve the data via the ESP-01S and apply it to the next cycle, rather than immediately. This ensures that each direction gets a fair turn based on actual traffic conditions

Technology Used
- Computer Vision: YOLOv11, RT-DETR, FCOS
- Server Deployment: AWS EC2 + FastAPI
- IoT Device: Raspberry Pi Pico + ESP-01S WiFi
- Decision Making: Fuzzy Logic (PCU-Based)
- Communication Protocol: HTTP Request (Pico → AWS)
- Traffic Light Hardware: Red–Yellow–Green LEDs for 4 directions (North, East, South, West)
