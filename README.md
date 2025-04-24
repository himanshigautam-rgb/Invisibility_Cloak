# Invisibility Cloak

This project implements a real-time invisibility cloak effect using Python, OpenCV, and Matplotlib. The program captures the background and replaces a specific color (e.g., red) in the video feed with the background, creating the illusion of invisibility.

## Features
- Real-time video processing.
- Detects a specific color (red by default) and replaces it with the background.
- Uses `matplotlib` for real-time visualization.

## Requirements
- Python 3.6 or higher
- Libraries:
  - OpenCV
  - NumPy
  - Matplotlib

## Installation
1. Clone or download this repository.
2. Install the required libraries:
   ```bash
   pip install opencv-python numpy matplotlib

### How to Run
- Open a terminal or command prompt.
- Navigate to the directory containing the script:
     cd C:\Users\dkvh2\Desktop\Cloak
- Run the script:
     python Cloak1.py

#### How It Works
- The program initializes the webcam and captures the background (a still scene without the cloak).
- It processes each frame in real-time to detect a specific color (red by default).
- The detected color is replaced with the captured background, creating the invisibility effect.
- The output is displayed in a real-time Matplotlib window.
#### Exiting the Program
- To exit the program, press Ctrl+C in the terminal.
#### Troubleshooting
- Webcam Not Detected: Ensure your webcam is connected and not being used by another application.
- Matplotlib Display Issues: Ensure matplotlib is installed and working correctly. Run pip install matplotlib if needed.
- Performance: For smoother performance, ensure your system has sufficient resources.


##### Example Output
When you wear a red cloak, the program will replace the red area with the captured background, making it appear as if you are invisible.

Enjoy your invisibility cloak project! 😊
       

   
