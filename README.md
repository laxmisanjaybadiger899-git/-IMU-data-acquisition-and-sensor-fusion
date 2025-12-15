# IMU Data Acquisition and Sensor Fusion

This project focuses on acquiring data from low-cost sensors — **MPU9250 (IMU)**, **HMC5883L (magnetometer)**, and **NEO-6M (GPS)** — and applying an **Extended Kalman Filter (EKF)** for sensor fusion.
The goal is to improve motion tracking accuracy by mitigating individual sensor limitations such as **IMU drift** and **GPS signal loss**.



## Project Objectives

* Acquire real-time data from MPU9250, HMC5883L, and NEO-6M sensors
* Perform sensor calibration to eliminate bias and offset
* Implement EKF for fusing accelerometer, gyroscope, magnetometer, and GPS data
* Estimate accurate **position, velocity, and orientation** in real time


## Hardware Components

## Hardware Setup

![Hardware Setup Diagram](images/image.png)


* **MPU9250** – 3-axis accelerometer and 3-axis gyroscope
* **HMC5883L** – 3-axis magnetometer
* **NEO-6M** – GPS module
* **Raspberry Pi** – Data acquisition and processing unit



## Sensor Calibration

To enhance estimation accuracy, all sensors are calibrated prior to fusion:

* **Accelerometer & Gyroscope**
  Offset is calculated using the average of **500 stationary samples**.

* **Magnetometer**
  Offset is derived by rotating the sensor in all directions and averaging readings over **10 seconds**.



## Sensor Fusion using Extended Kalman Filter (EKF)

The EKF is used to combine measurements from multiple sensors and produce a reliable state estimate.

### EKF Functions

* Predict motion state using IMU data
* Correct predicted state using GPS measurements
* Apply yaw correction using magnetometer data



## State Vector

* **x, y** – Position
* **vx, vy** – Velocity
* **yaw** – Orientation angle



## EKF Processing Flow

1. Read raw sensor values
2. Convert GPS latitude and longitude to **UTM coordinates (meters)**
3. Predict motion state using accelerometer and gyroscope data
4. Update state using GPS measurements
5. Apply yaw correction using magnetometer data
6. Save and export filtered EKF output


## Output and Accuracy

![EKF Output Path](images/ekf_output.png)

* **Red Path** – GPS logger path (mobile phone reference)
* **Blue Path** – Raw sensor path (MPU9250 + NEO-6M + HMC5883L)
* **Green Path** – EKF filtered output

**Average error between raw GPS and EKF output: 5.13 meters**


## Dataset

* Raw sensor data logs (CSV):
  [Download](https://drive.google.com/file/d/1MSZc2ri92wEc8Nm7qAl5g8xDtpZ0N0Op/view?usp=drivesdk)

* Filtered EKF output:
  [Download](https://drive.google.com/file/d/1MR0PKdPoQW8ihD3Qlb1ICvZ5o_7j_QCj/view?usp=drivesdk)

* GPS logger reference data:
  [Download](https://drive.google.com/file/d/1MT03GHJNlI-IB70fbP5GRPpZ1tv4qIla/view?usp=drivesdk)

---

## Applications

* Real-time motion tracking for robots and autonomous vehicles
* Precision agriculture and asset tracking
* Drone localization in GPS-denied environments

---

## Hardware Setup

![Hardware Setup 1](images/hardware_setup_1.jpg)
![Hardware Setup 2](images/hardware_setup_2.jpg)

---

## Results

![Result Visualization](images/result.png)

---

## Future Enhancements

* Real-time implementation on microcontrollers
* Integration of additional sensors such as **barometers** or **LiDAR**
* Adaptive filtering based on terrain and environmental conditions
