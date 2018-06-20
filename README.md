#### Problems and solutions when prepare the Simulator
1. Install Ubuntu for Windows
2. Install cmake, openssl, and libssl-dev
  ```
  sudo apt-get install cmake
  sudo apt-get install openssl
  sudo apt-get install libssl-dev
  ```
3. In the repository run `./install-ubuntu.sh` to install the _uWS_
3. Use `g++ -std=c++11 test.cpp -o test` in Ubuntu window CML to compile, otherwise always prompt "fatal error: uWS/uWS.h: No such file or directory"
4. Build at the top level of the project repository `mkdir build` && `cd build`
from ``/build cmake ..`` && `make`

#### Files in the Github src Folder
The files you need to work with are in the src folder of the github repository.

* main.cpp - communicates with the Term 2 Simulator receiving data measurements, calls a function to run the Kalman filter, calls a function to calculate RMSE
* FusionEKF.cpp - initializes the filter, calls the predict function, calls the update function
* kalman_filter.cpp- defines the predict function, the update function for lidar, and the update function for radar
* tools.cpp- function to calculate RMSE and the Jacobian matrix
The only files you need to modify are FusionEKF.cpp, kalman_filter.cpp, and tools.cpp.

#### How the Files Relate to Each Other
Here is a brief overview of what happens when you run the code files:

* Main.cpp reads in the data and sends a sensor measurement to FusionEKF.cpp
* FusionEKF.cpp takes the sensor data and initializes variables and updates variables. The Kalman filter equations are not in this file. FusionEKF.cpp has a variable called ekf_, which is an instance of a KalmanFilter class. The ekf_ will hold the matrix and vector values. You will also use the ekf_ instance to call the predict and update equations.
* The KalmanFilter class is defined in kalman_filter.cpp and kalman_filter.h. You will only need to modify 'kalman_filter.cpp', which contains functions for the prediction and update steps.
