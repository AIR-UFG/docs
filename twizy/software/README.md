## Software Documentation

This repository contains software components essential for the operation and development of the StreetDrone Renault Twizy. It encompasses the operating system configuration, as well as the Vehicle Interface responsible for communication between the Twizy and ROS-based self-driving software stacks.

### Operating System Configuration

For instructions on configuring the operating system environment for the StreetDrone Renault Twizy, including Ubuntu installation and Docker setup, please refer to the [Operating System Documentation](software/operating_system.md).

### Vehicle Interface

The Vehicle Interface facilitates communication between StreetDrone vehicles and ROS-based self-driving software stacks. It acts as a bridge between ROS and the OpenCAN vehicle interface of the StreetDrone Xenos Control Unit (XCU) integrated into the Twizy and other StreetDrone vehicles.

#### Package Information

For detailed information about the Vehicle Interface package, including its functionalities and usage, you can refer to the 

- Original Repository: [StreetDrone Vehicle Interface](https://github.com/streetdrone-home/SD-VehicleInterface/)
- The fork utilized by our team from Monash University: [Monash-Connected-Autonomous-Vehicle Vehicle Interface](https://github.com/Monash-Connected-Autonomous-Vehicle/SD-VehicleInterface/)

#### Running on the Vehicle

To run the Vehicle Interface on the StreetDrone Renault Twizy, utilize our dockerized version of the package available in our [vehicle_interface_docker](https://github.com/AIR-UFG/vehicle_interface_docker) repository. This repository contains the necessary Dockerfile and instructions for building and running the Vehicle Interface on the Twizy.

For further instructions and guidance on setting up and utilizing the Vehicle Interface, please refer to the respective repositories.

By following the provided documentation, you can effectively configure the operating system environment and utilize the Vehicle Interface to enable communication between the Twizy and ROS-based self-driving software stacks.