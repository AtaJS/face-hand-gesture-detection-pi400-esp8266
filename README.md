# Face-Gesture Recognition Using OpenCV on Raspberry Pi 400 with ESP8266 Network Module

## Project Description
This project uses a camera to recognize familiar faces and certain hand gestures, with each gesture associated with a specific command. The command is issued if the recognized face's name is in the `confirmed_names` list and the hand gesture is linked with that command.

This project has two parts:

1. **The Python Script (multi_thread.py)**: 
    - Uses the `face_recognition` package to recognize faces. It uses `.png` files of faces in the `/faces` directory for recognition. For example, it would label a face that matches `joe.png` as `joe`.
    - Detects hand gestures using the `mp_hand_gesture` model (a Keras model).
    - The entire process runs in threads that execute concurrently.

    **Note**: To run the code properly, you should modify the following parts:
    - `.png` files in the `/faces` directory (place `.png` files of faces you want the code to recognize).
    - `self.url` value in the `tcp_call` class (multi_thread.py line 105), place the address of your ESP board (or whatever) in the network.
    - Names in the `self.confirmed_names` list (multi_thread.py line 173). The code will respond to those faces whose names are in this list only.

2. **ESP Board Programmed as Server**:
    - The ESP board waits for requests from the Python script.
    - The main idea is that the Python script sees familiar people making certain hand gestures and sends a request to the ESP board. This can be used, for example, to turn an LED on and off.

**It's highly recommended to create a virtual environment for running the code.**

## Code Description

### Python Code (Raspberry Pi 400)
The Python code is responsible for face and gesture recognition using a webcam. It utilizes the following libraries:
- `face_recognition`: Provides face detection and recognition functions.
- `cv2` (OpenCV): Provides computer vision and image processing functions.
- `numpy`: Provides numerical and array manipulation functions.
- `math`: Provides mathematical functions.
- `mediapipe`: Provides machine learning solutions for various tasks, such as hand and face tracking.
- `tensorflow`: Provides a framework for deep learning and neural networks.
- `requests`: Provides functions for sending HTTP requests to web servers.
- `threading`: Provides a class that creates and manages a new thread of execution.
- `datetime`: Provides functions for working with dates and times.

### C++ Code (ESP8266)
The C++ code is responsible for connecting the ESP8266 board to a Wi-Fi network and controlling an LED based on HTTP requests. It uses the following library:
- `ESP8266WiFi`: Provides WiFi functions for the ESP8266 board.

## How It Works
1. The Python code captures video frames from a webcam and processes them to detect and recognize faces and hand gestures.
2. When a thumbs-up gesture is detected, the system sends a request to the ESP8266 to turn on the LED.
3. When a thumbs-down gesture is detected, the system sends a request to the ESP8266 to turn off the LED.

## Conclusion
This project demonstrates the integration of face and gesture recognition with IoT devices, showcasing the potential for creating interactive and responsive systems using readily available hardware and software libraries.
