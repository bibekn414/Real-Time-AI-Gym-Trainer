# Real-Time AI Gym Trainer

A real-time AI-powered fitness coaching system that uses **Computer Vision, Human Pose Estimation, Exercise Form Analysis, Repetition Tracking, and Generative AI** to monitor workouts through a webcam and provide real-time visual and voice feedback.

## Live Demo

**Try the application here:**  
[https://ai-realtime-gym-coach.streamlit.app/](https://ai-realtime-gym-coach.streamlit.app/)

**GitHub Repository:**  
[https://github.com/bibekn414/Real-Time-AI-Gym-Trainer](https://github.com/bibekn414/Real-Time-AI-Gym-Trainer)

---

## Project Overview

**Real-Time AI Gym Trainer** is a computer vision-based fitness application designed to monitor a user's workout through a webcam and provide real-time exercise analysis.

The application uses **MediaPipe Pose Landmarker** to identify human body landmarks from live video frames. These landmarks are processed by exercise-specific detection modules to calculate joint angles, identify different stages of an exercise, count repetitions, monitor sets, and evaluate exercise form.

The system also integrates a **Large Language Model (LLM)** through the Groq API to generate short and contextual coaching instructions. These instructions can be converted into speech so that users receive feedback while exercising without continuously looking at the screen.

The application currently supports five exercises:

- Squats
- Push-ups
- Biceps Curls
- Shoulder Press
- Lunges

The project combines **Computer Vision, Pose Estimation, Real-Time Video Processing, Geometric Feature Engineering, Rule-Based Exercise Analysis, LLM Integration, Text-to-Speech, and Web Application Development** into a single fitness coaching platform.

---

## Problem Statement

People often perform exercises without continuous supervision from a fitness trainer.

During unsupervised workouts, users may experience problems such as:

- Incorrect exercise posture
- Improper range of motion
- Incorrect repetition counting
- Poor body alignment
- Excessive body movement
- Inconsistent workout tracking
- Lack of immediate feedback

Traditional fitness applications generally record workout information but cannot continuously observe the user's body movement through a camera.

This project addresses this problem by building an AI-powered virtual gym trainer capable of analyzing body posture and exercise movements in real time.

---

## Objective

The main objective of this project is to develop an intelligent fitness coaching system that can:

- Capture live workout video through a webcam
- Detect human body landmarks
- Track important joints during exercise
- Calculate joint angles and body geometry
- Identify different exercise movement stages
- Count repetitions automatically
- Track workout sets
- Evaluate exercise form
- Detect selected posture problems
- Display real-time exercise metrics
- Generate AI-based coaching feedback
- Convert coaching feedback into speech
- Maintain workout history for users

The overall goal is to demonstrate how **Computer Vision and Generative AI** can be integrated to build an interactive real-time fitness application.

---

# Key Features

## Real-Time Human Pose Estimation

The system uses MediaPipe Pose Landmarker to detect body landmarks from live webcam frames.

These landmarks represent important body locations such as:

- Shoulders
- Elbows
- Wrists
- Hips
- Knees
- Ankles
- Feet

The detected landmarks are used for exercise analysis.

---

## Live Webcam Processing

The application uses **Streamlit WebRTC** to capture live webcam video directly from the user's browser.

Each incoming video frame is processed by the computer vision pipeline before being displayed back to the user.

---

## Skeleton Visualization

The application draws a pose skeleton over the detected user.

The skeleton connects important landmarks across:

- Arms
- Shoulders
- Torso
- Hips
- Legs

This provides a visual representation of the body landmarks being analyzed by the system.

---

## Joint Angle Calculation

Body landmark coordinates are used to calculate joint and posture angles.

Depending on the selected exercise, the system analyzes parameters such as:

- Knee angle
- Elbow angle
- Back angle
- Torso angle
- Arm extension
- Hip position

These geometric features are used to evaluate exercise movement.

---

## Automatic Repetition Counting

Exercise-specific detectors identify different movement states.

A repetition is counted when the user successfully completes the required movement cycle.

The general process is:

```text
Body Landmarks
      |
      v
Joint Angles
      |
      v
Movement State
      |
      v
Exercise Phase Transition
      |
      v
Completed Repetition
```

---

## Set Tracking

Users can define:

- Target number of sets
- Repetitions per set

The system then tracks:

- Total repetitions
- Current set repetitions
- Completed sets
- Target sets

---

## Exercise Form Analysis

The application analyzes exercise-specific body parameters to provide feedback about the user's movement.

Examples include:

- Squat depth
- Push-up body alignment
- Hip position
- Shoulder stability
- Arm swing
- Arm extension
- Back arch
- Lunge balance

---

## AI Coaching

The application integrates the **Groq API** with an LLM-based coaching module.

Workout events and detected form issues can be sent to the AI coach, which generates short natural-language feedback.

---

## Voice Coaching

Generated AI feedback is passed through a text-to-speech pipeline.

This allows coaching instructions to be delivered as audio while the user is exercising.

---

## Workout History

The application maintains workout records for authenticated users.

Workout information includes:

- Exercise
- Repetitions
- Sets
- Workout duration
- Date

---

# Supported Exercises

The current version supports **five exercises**.

| Exercise | Main Metrics |
|---|---|
| Squats | Knee Angle, Back Angle, Depth Status |
| Push-ups | Elbow Angle, Body Alignment, Hip Position |
| Biceps Curls | Elbow Angle, Shoulder Stability, Swing Detection |
| Shoulder Press | Elbow Angle, Arm Extension, Back Arch |
| Lunges | Front Knee Angle, Torso Angle, Balance Status |

---

# How the System Works

The complete application pipeline can be summarized as follows:

```text
User
  |
  v
Webcam
  |
  v
Streamlit WebRTC
  |
  v
Live Video Frames
  |
  v
OpenCV Frame Processing
  |
  v
MediaPipe Pose Landmarker
  |
  v
Human Body Landmarks
  |
  v
Exercise-Specific Detector
  |
  +-------------------------+
  |                         |
  v                         v
Joint Angle             Form Analysis
Calculation
  |                         |
  +------------+------------+
               |
               v
       Movement Detection
               |
               v
        Repetition Counter
               |
               v
          Set Tracking
               |
               v
        Workout Metrics
               |
        +------+------+
        |             |
        v             v
   User Interface   AI Coach
                      |
                      v
                   Groq LLM
                      |
                      v
               Coaching Response
                      |
                      v
                Text-to-Speech
                      |
                      v
                Voice Feedback
```

---

# System Architecture

The project follows a modular architecture where different components handle different responsibilities.

```text
                         USER
                           |
                           v
                    Streamlit UI
                           |
             +-------------+-------------+
             |                           |
             v                           v
      Workout Configuration        Authentication
             |
             v
       Streamlit WebRTC
             |
             v
        Webcam Frames
             |
             v
     Video Processor Class
             |
             v
   MediaPipe Pose Landmarker
             |
             v
       Pose Landmarks
             |
             v
    Exercise Detector Layer
             |
     +-------+-------+
     |       |       |
     v       v       v
   Angles   Reps   Form
     |       |       |
     +-------+-------+
             |
             v
        Workout Metrics
             |
      +------+------+
      |             |
      v             v
Persistence      AI Coaching
                    |
                    v
                 Groq LLM
                    |
                    v
              Text-to-Speech
```

---

# Computer Vision Pipeline

## Step 1: Webcam Capture

The browser webcam is accessed through Streamlit WebRTC.

The application continuously receives frames while the workout session is active.

---

## Step 2: Frame Processing

Incoming frames are converted into a format suitable for OpenCV and MediaPipe processing.

The video frame is also horizontally flipped to provide a natural mirror-like workout experience.

---

## Step 3: Pose Detection

MediaPipe Pose Landmarker processes each frame.

The application uses the full pose landmarker model:

```text
pose_landmarker_full.task
```

The pose estimator identifies human body landmarks required for movement analysis.

---

## Step 4: Landmark Visibility Checking

The application checks landmark visibility before using points for skeleton visualization.

Low-confidence or poorly visible landmarks are not treated the same as clearly detected landmarks.

This helps reduce unreliable visual information.

---

## Step 5: Skeleton Drawing

OpenCV is used to draw lines between selected pose landmarks.

The displayed skeleton includes important connections across the:

- Arms
- Shoulders
- Torso
- Hips
- Legs

---

## Step 6: Exercise Selection

The user's selected exercise determines which detector receives the pose landmarks.

The available detectors are:

```text
SquatDetector
PushUpDetector
BicepsCurlDetector
ShoulderPressDetector
LungesDetector
```

---

## Step 7: Geometric Feature Extraction

Exercise-specific detectors calculate important geometric measurements from pose landmarks.

Examples include:

```text
Knee Angle
Elbow Angle
Back Angle
Torso Angle
Hip Position
Arm Extension
```

---

## Step 8: Movement Analysis

The calculated measurements are compared with exercise-specific movement rules.

The system determines the current movement stage and evaluates selected aspects of exercise form.

---

## Step 9: Repetition Detection

A repetition is recorded after the expected movement cycle has been completed.

This prevents the system from simply counting every video frame as a repetition.

---

## Step 10: Metrics Synchronization

Exercise metrics generated inside the video processing pipeline are synchronized with the Streamlit session.

These values are displayed in the application's workout interface.

---

# Exercise Analysis

## Squats

The squat detector analyzes lower-body and torso movement.

The primary metrics displayed by the application include:

```text
Knee Angle
Back Angle
Depth Status
```

### General Processing

```text
Pose Detection
      |
      v
Hip/Knee/Ankle Landmarks
      |
      v
Knee Angle Calculation
      |
      v
Squat Phase Detection
      |
      v
Depth Evaluation
      |
      v
Rep Counting
```

The system also displays squat depth information over the video stream.

---

## Push-ups

The push-up detector focuses on upper-body movement and body alignment.

The primary metrics include:

```text
Elbow Angle
Body Alignment
Hip Position
```

### General Processing

```text
Pose Detection
      |
      v
Shoulder/Elbow/Wrist/Hip Landmarks
      |
      v
Elbow Angle
      |
      v
Body Alignment Analysis
      |
      v
Movement State
      |
      v
Rep Counting
```

---

## Biceps Curls

The biceps curl detector analyzes elbow flexion and selected upper-body movement.

The primary metrics include:

```text
Elbow Angle
Shoulder Stability
Swing Detection
```

### General Processing

```text
Pose Detection
      |
      v
Shoulder/Elbow/Wrist Landmarks
      |
      v
Elbow Angle
      |
      v
Curl Movement State
      |
      v
Swing Analysis
      |
      v
Rep Counting
```

---

## Shoulder Press

The shoulder press detector monitors pressing movement and posture.

The primary metrics include:

```text
Elbow Angle
Arm Extension
Back Arch
```

### General Processing

```text
Pose Detection
      |
      v
Upper Body Landmarks
      |
      v
Elbow Angle
      |
      v
Arm Extension Analysis
      |
      v
Back Position Analysis
      |
      v
Rep Counting
```

---

## Lunges

The lunge detector analyzes lower-body posture and balance.

The primary metrics include:

```text
Front Knee Angle
Torso Angle
Balance Status
```

### General Processing

```text
Pose Detection
      |
      v
Hip/Knee/Ankle Landmarks
      |
      v
Front Knee Angle
      |
      v
Torso Analysis
      |
      v
Balance Evaluation
      |
      v
Rep Counting
```

---

# AI Coaching System

The project contains an LLM-based AI coaching component.

The AI coaching system is implemented using the **Groq API**.

The current model configured in the project is:

```text
llama-3.3-70b-versatile
```

The AI coach receives workout events and detected form issues.

Examples of supported events include:

```text
workout_started
set_completed
workout_completed
no_pose_detected
ongoing_form_check
```

The general AI coaching workflow is:

```text
Workout Event
      |
      v
Exercise Metrics
      |
      v
Detected Form Issue
      |
      v
Prompt Construction
      |
      v
Groq API
      |
      v
Llama LLM
      |
      v
Short Coaching Message
```

The prompt is designed to generate short, natural and encouraging workout instructions suitable for real-time coaching.

---

# Voice Feedback

The project includes a text-to-speech pipeline.

After the AI coach generates a response, the feedback can be converted into audio.

```text
Detected Workout Event
        |
        v
     LLM Coach
        |
        v
   Text Response
        |
        v
 Text-to-Speech
        |
        v
   Audio Output
        |
        v
      User
```

This allows users to receive feedback without continuously looking at the computer screen.

---

# Workout Tracking

Before starting an exercise, the user selects:

```text
Exercise
Number of Sets
Repetitions per Set
```

After the workout begins, the application tracks:

```text
Total Reps
Current Set Reps
Sets Completed
Target Sets
```

Exercise-specific measurements are also displayed in real time.

---

# Workout History

The application contains a persistence layer for storing workout information.

For each user, workout records can contain:

```text
Exercise Name
Repetitions
Sets
Workout Time
Date
```

Pandas is used to organize and aggregate workout history before displaying it in the application.

Workout information can therefore be reviewed after completing training sessions.

---

# Authentication

The main application contains a login system.

The login wall is displayed before the workout application becomes available.

After authentication, user-related session information is initialized.

This allows workout records to be associated with the logged-in user.

---

# Technologies Used

## Programming Language

- Python

## Computer Vision

- MediaPipe
- OpenCV
- NumPy

## Pose Estimation

- MediaPipe Tasks
- Pose Landmarker

## Web Application

- Streamlit
- Streamlit WebRTC

## Generative AI

- Groq API
- Llama 3.3 70B

## Data Processing

- Pandas

## Voice Processing

- gTTS
- Text-to-Speech Pipeline

## Frontend

- Streamlit
- HTML
- CSS

## Development Tools

- Git
- GitHub
- VS Code
- Python Virtual Environment
- Python Dotenv

---

# Python Dependencies

The main application currently uses the following dependencies:

```text
streamlit==1.54.0
streamlit-webrtc==0.64.5
mediapipe==0.10.14
opencv-python-headless==4.10.0.84
pandas==2.2.3
groq>=0.12.0
gtts==2.5.3
python-dotenv==1.2.2
```

These dependencies are available in:

```text
Main App/requirements.txt
```

---

# Project Structure

```text
Real-Time-AI-Gym-Trainer/
│
├── LandingPage/
│   │
│   ├── IMGs_add_your_own/
│   ├── fonts/
│   ├── index.html
│   ├── style.css
│   └── videos_add_your_own/
│
├── Main App/
│   │
│   ├── core/
│   │
│   ├── detectors/
│   │   ├── __init__.py
│   │   ├── squat.py
│   │   ├── pushup.py
│   │   ├── biceps_curl.py
│   │   ├── shoulder_press.py
│   │   └── lunges.py
│   │
│   ├── ml_models/
│   │   └── pose_landmarker_full.task
│   │
│   ├── pages/
│   │
│   ├── services/
│   │   ├── auth/
│   │   ├── coaching/
│   │   ├── config/
│   │   ├── persistence/
│   │   ├── state/
│   │   ├── tracking/
│   │   ├── ui/
│   │   └── vision/
│   │
│   ├── static/
│   ├── tutorial-info/
│   ├── main.py
│   ├── packages.txt
│   └── requirements.txt
│
├── .gitignore
└── README.md
```

---

# Installation and Setup

Follow the steps below to run the project locally.

## Step 1: Clone the Repository

Open a terminal and run:

```bash
git clone https://github.com/bibekn414/Real-Time-AI-Gym-Trainer.git
```

---

## Step 2: Enter the Repository

```bash
cd Real-Time-AI-Gym-Trainer
```

---

## Step 3: Enter the Main Application Directory

The Streamlit application is located inside the `Main App` directory.

```bash
cd "Main App"
```

---

## Step 4: Create a Virtual Environment

### Windows

```bash
python -m venv venv
```

Activate the environment:

```bash
venv\Scripts\activate
```

### macOS/Linux

```bash
python3 -m venv venv
```

Activate the environment:

```bash
source venv/bin/activate
```

---

## Step 5: Upgrade pip

```bash
python -m pip install --upgrade pip
```

---

## Step 6: Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Step 7: Configure the Groq API Key

The AI coaching functionality requires a Groq API key.

Create a `.env` file inside the `Main App` directory.

Add:

```env
GROQ_API_KEY=your_groq_api_key
```

Replace:

```text
your_groq_api_key
```

with your own API key.

Do not upload API keys or secret credentials to a public GitHub repository.

---

# How to Run the Project

After completing the installation, make sure your terminal is inside:

```text
Real-Time-AI-Gym-Trainer/Main App
```

Run:

```bash
streamlit run main.py
```

Streamlit will start the application.

The local application is normally available at:

```text
http://localhost:8501
```

Open the address in your browser.

---

# How to Use the Application

## Step 1: Open the Application

Use either the deployed application:

[https://ai-realtime-gym-coach.streamlit.app/](https://ai-realtime-gym-coach.streamlit.app/)

or run the application locally.

---

## Step 2: Login

Complete the authentication process to access the workout interface.

---

## Step 3: Select an Exercise

Choose an exercise from the sidebar.

Available exercises are:

```text
Squats
Push-ups
Biceps Curls (Dumbbell)
Shoulder Press
Lunges
```

---

## Step 4: Configure the Workout

Enter the desired:

```text
Sets
Repetitions per Set
```

---

## Step 5: Start the Workout

Click:

```text
Start Workout
```

The application will initialize the workout session.

---

## Step 6: Allow Camera Access

Your browser may ask for permission to access the webcam.

Allow camera access for real-time pose analysis.

---

## Step 7: Position Yourself Correctly

Make sure the relevant parts of your body are visible inside the camera frame.

For better results:

- Use sufficient lighting
- Keep the camera stable
- Avoid excessive background movement
- Keep important joints visible
- Maintain an appropriate distance from the camera
- Avoid objects blocking your body

---

## Step 8: Perform the Exercise

Perform the selected exercise normally.

The application processes the video stream and analyzes the detected body landmarks.

---

## Step 9: Monitor Real-Time Metrics

Depending on the selected exercise, the application displays information such as:

```text
Total Repetitions
Current Set Repetitions
Completed Sets
Joint Angles
Body Alignment
Exercise Form Status
```

---

## Step 10: Receive AI Coaching

Workout events and selected form issues can trigger the AI coaching pipeline.

The generated feedback can be played as audio.

---

## Step 11: Complete the Workout

After completing the session, click:

```text
End Workout
```

---

## Step 12: Review Workout History

The workout history section displays previous workout information associated with the user.

---

# MediaPipe Configuration

The computer vision pipeline initializes MediaPipe Pose Landmarker in video mode.

The application uses confidence thresholds for:

```text
Pose Detection Confidence: 0.7
Pose Presence Confidence: 0.7
Tracking Confidence: 0.7
```

The full pose landmarker model is loaded from:

```text
ml_models/pose_landmarker_full.task
```

---

# No-Pose Detection

If the system cannot detect a valid pose, the video processor displays a warning.

The user should:

- Move into the camera frame
- Ensure the relevant body parts are visible
- Improve lighting
- Adjust camera position
- Reduce occlusion

Once the pose becomes visible again, exercise analysis can continue.

---

# Why MediaPipe?

MediaPipe is suitable for this application because it provides efficient human pose estimation for real-time applications.

Pose landmarks can be converted into geometric features that help analyze exercise movement.

Instead of processing raw pixels alone, the exercise detectors can work with meaningful body coordinates.

This allows the application to calculate:

- Joint angles
- Body alignment
- Movement phases
- Range of motion
- Posture-related features

---

# Why OpenCV?

OpenCV is used for real-time image and video processing.

It helps the application perform operations such as:

- Frame conversion
- Frame flipping
- Skeleton drawing
- Landmark visualization
- Text overlays
- Real-time visual feedback

---

# Why Streamlit?

Streamlit provides a Python-based interface for rapidly building interactive machine learning applications.

It is used to create:

- Workout configuration controls
- Exercise selection
- Workout metrics
- User feedback
- Workout history
- Application state management

---

# Why Streamlit WebRTC?

Real-time workout analysis requires continuous video streaming.

Streamlit WebRTC enables the browser webcam to continuously send frames to the application's video processing pipeline.

The workflow becomes:

```text
Browser Camera
      |
      v
WebRTC Stream
      |
      v
Python Video Processor
      |
      v
Computer Vision
      |
      v
Processed Video
      |
      v
Browser
```

---

# Why Exercise-Specific Detectors?

Different exercises depend on different body joints and movement patterns.

For example:

```text
Squats
→ Knee + Hip + Torso Geometry

Push-ups
→ Shoulder + Elbow + Hip Alignment

Biceps Curls
→ Shoulder + Elbow + Wrist Movement

Shoulder Press
→ Shoulder + Elbow + Upper Body Posture

Lunges
→ Hip + Knee + Ankle + Torso Geometry
```

Therefore, the project uses separate detector modules instead of applying the same movement rules to every exercise.

This modular design also makes it easier to add additional exercises.

---

# Key Technical Concepts Demonstrated

This project demonstrates practical implementation of several Computer Vision and AI concepts:

- Computer Vision
- Human Pose Estimation
- Pose Landmark Detection
- Real-Time Video Processing
- Image Processing
- Joint Angle Calculation
- Geometric Feature Engineering
- Human Movement Analysis
- Exercise State Detection
- Repetition Counting
- Exercise Form Analysis
- WebRTC Streaming
- Session State Management
- Data Persistence
- Large Language Model Integration
- Prompt Engineering
- Generative AI
- Text-to-Speech
- Real-Time AI Applications
- Modular Python Development

---

# Current Limitations

The current system has several practical limitations.

### Camera Dependence

Pose detection performance depends on the camera position and viewing angle.

### Lighting Conditions

Poor lighting may reduce pose landmark quality.

### Occlusion

If important body joints are hidden, exercise analysis may become unreliable.

### Exercise Coverage

The current version supports five predefined exercises.

### Rule-Based Exercise Analysis

Exercise-specific form evaluation relies on geometric measurements and predefined logic.

### User Variation

Body proportions and exercise techniques vary between users, so fixed thresholds may not work equally well for everyone.

### Internet Requirement

The AI coaching functionality requires access to the external LLM service.

### API Availability

AI feedback depends on Groq API availability and configuration.

### Single-Person Focus

The current architecture is primarily designed to analyze one exercising user.

---

# Future Improvements

The project can be extended with several features.

## Automatic Exercise Recognition

A future version could automatically recognize the exercise instead of requiring manual selection.

## Additional Exercises

Support can be extended to exercises such as:

- Planks
- Deadlifts
- Jumping Jacks
- Triceps Extensions
- Lateral Raises
- Burpees
- Sit-ups

## Personalized Calibration

Movement thresholds could be calibrated according to individual body proportions and mobility.

## Exercise Quality Score

The system could generate a numerical form score for each repetition.

## Progress Analytics

Historical workout information could be visualized using dashboards and charts.

## Personalized Workout Recommendations

The system could recommend workouts based on previous performance.

## Adaptive AI Coaching

AI feedback could become personalized according to user performance and workout history.

## Automatic Error Classification

Machine learning models could be trained to classify different exercise form errors.

## Action Recognition

Deep learning-based action recognition could complement the existing pose-based movement analysis.

## Mobile Application

The system could be converted into a mobile-friendly fitness application.

## Offline AI

Future versions could explore local models to reduce dependence on external APIs.

## Performance Optimization

The computer vision pipeline could be further optimized for lower latency and more resource-constrained devices.

---

# Potential Applications

The architecture demonstrated in this project could be extended beyond a basic gym application.

Potential applications include:

- Virtual fitness coaching
- Home workout monitoring
- Exercise repetition tracking
- Sports movement analysis
- Physical activity analytics
- Fitness technology research
- Human movement analysis
- Interactive AI coaching systems

---

# Deployment

The application is deployed using Streamlit.

## Live Application

[https://ai-realtime-gym-coach.streamlit.app/](https://ai-realtime-gym-coach.streamlit.app/)

The deployed application requires browser camera permission for real-time pose estimation.

For AI coaching functionality, the required API credentials must also be configured securely in the deployment environment.

---

# Repository

The complete source code is available at:

[https://github.com/bibekn414/Real-Time-AI-Gym-Trainer](https://github.com/bibekn414/Real-Time-AI-Gym-Trainer)

---

# Author

**Bibek Nayak**

GitHub: [bibekn414](https://github.com/bibekn414)

Project Repository:  
[Real-Time AI Gym Trainer](https://github.com/bibekn414/Real-Time-AI-Gym-Trainer)

Live Demo:  
[https://ai-realtime-gym-coach.streamlit.app/](https://ai-realtime-gym-coach.streamlit.app/)
