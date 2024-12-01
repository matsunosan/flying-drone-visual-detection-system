# **Flying Drone Visual Detection System**  
*A real-time object detection and classification system for UAVs (Unmanned Aerial Vehicles), designed for military and surveillance applications.*

## **Project Overview**  
The **Flying Drone Visual Detection System** is a computer vision-based system that enables UAVs to detect, classify, and differentiate between various objects in real-time. The system is built using deep learning models, integrated with ROS (Robot Operating System), and tested in both simulation and real-world environments.

### **Key Features**  
- **Real-time Object Detection**: Utilizes the YOLOv5 architecture for fast and accurate object detection.  
- **Customizable Classes**: Detects a variety of objects such as vehicles, tanks, buildings, and personnel.  
- **Simulation Integration**: Tested in the Gazebo simulation environment for robust performance.  
- **ROS-Based System**: Seamlessly integrates with UAVs using ROS for communication and control.

---

## **Project Structure**  
The repository is structured as follows:

```plaintext
├── data/                   # Dataset and annotations
├── docs/                   # Documentation and reports
├── models/                 # Pretrained and fine-tuned models
├── scripts/                # Python scripts for training, detection, and integration
├── simulation/             # Gazebo simulation files
├── src/                    # ROS nodes for object detection
├── results/                # Test results and evaluation metrics
└── README.md               # Project overview and setup instructions
```

---

## **Installation and Setup**  

Follow the instructions below to set up the system on your local machine.

### **1. Clone the Repository**  
```bash
git clone https://github.com/matsunosan/flying-drone-visual-detection-system.git
cd flying-drone-visual-detection-system
```

### **2. Install Dependencies**  
This project requires Python 3.8 or higher, along with the following dependencies:

```bash
pip install -r requirements.txt
```

Key libraries:  
- `torch`  
- `opencv-python`  
- `numpy`  
- `matplotlib`  
- `rospy` (for ROS integration)

### **3. Set Up ROS**  
Ensure ROS Noetic is installed and properly configured.  
```bash
sudo apt-get install ros-noetic-desktop-full
```

### **4. Running the System**  

#### **4.1 Running in Simulation (Gazebo)**  
Launch the simulation environment:  
```bash
roslaunch simulation drone_simulation.launch
```

Run the object detection node:  
```bash
rosrun src object_detection_node.py
```

#### **4.2 Running on Physical UAV**  
1. Deploy the model to the UAV’s onboard computer.  
2. Run the object detection script.  
3. Monitor detected objects via the ROS topic `/detected_objects`.

---

## **Testing and Evaluation**  

### **Simulation Testing**  
Test the system in the Gazebo simulation environment with different objects and scenarios.  

### **Real-World Testing**  
Deploy the system on a UAV and conduct field tests to evaluate detection accuracy and system performance.

---

## **Future Work**  
- **Expand Object Classes**: Incorporate more object categories and improve detection accuracy.  
- **Optimize Inference Speed**: Enhance real-time performance on low-power devices.  
- **Integrate Thermal Imaging**: Add thermal cameras for night-time object detection.

---

## **License**  
All rights reserved. This project is proprietary and may not be used, modified, or distributed without permission from the owner.  

---

## **Contact**  
For any inquiries or collaboration opportunities, please reach out via [GitHub Issues](https://github.com/matsunosan/flying-drone-visual-detection-system/issues).
