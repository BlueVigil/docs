# Documentation of Blue Vigil

## Table of Contents
- [Introduction](#introduction)
- [Update Sequence](#update-sequence)]
  - [Drone System](#drone-system)
    - [MavProxy](#mavproxy)
    - [Mission Controller](#mission-controller)
    - [MavProxy Commander](#mavproxy-commander)
  - [Ground Station System](#ground-station)
    - [GCS Board](#gcs-board)
    - [Pendant](#pendant)
    - [ALED Power Board](#aled-power-board)

## Introduction
Lorem ipsum dolor sit amet, consectetur adipiscing elit

## Update Sequence
The update sequence is kicked off by the user connecting the *standalone* **Updater Board** to the exposed USB port on the drone. The **Updater Board** is powered by the drone and is capable of updating the drone's onboard software. The software is bundled into Docker Images and is stored on the **Updater Board**.
The Update sequence for the drone is as follows:

<!-- Update Sequence Diagram -->
![Update Sequence Diagram](images/UpdateSequence.drawio.svg)

**Drone Update Sequence**
1. The **Updater Board** is connected to the drone.
2. The **Updater Board** checks for running containers that matched the **Updater Board**'s Docker Images.
3. The **Updater Board** stops the running containers.
4. The **Updater Board** loads the Docker Images onto the drone.
5. Using the defined Docker Compose file, the **Updater Board** starts the containers on the drone.
6. The **Updater Board** disconnects from the drone.

**Ground Station Update Sequence**
1. The **Updater Board** is connected to the drone.
2. The **Updater Board** loads each hex file onto the drone.
3. The drone begins sending a ***JSON*** message to each connected ground station device.
4. The ground station devices establish an FTP server and wait for the drone to connect.
5. The drone connects to the FTP server and sends the hex file to the ground station device where each hex file is stored within the devices' SD card.
6. Once the hex file is stored, the device checks the integrity of the file.
7. The device sends a ***JSON*** message to the drone indicating the file was stored successfully.
8. The drone disconnects from the FTP server.
9. Each device(s) enters an update sequence where the the hex file is written into a buffer on the flash memory.
10. The device(s) writes the hex file to the flash memory updating the device's firmware.
11. The device(s) reboot and check the integrity of the firmware.

### Drone System

#### MavProxy

#### Mission Controller

#### MavProxy Commander

### Ground Station System

#### GCS Board

#### Pendant

#### ALED Power Board
