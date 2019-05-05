# Real time estimation and visualisation of road terrain

## Problem Analysis
### Motivation
Web mapping services like Google Maps display an immense amount of information like the best route between two points at any given time, real time updates of the traffic on a route, elevation etc.

However, they do not convey any information about the terrain of the route.  Following are the reasons why solving this problem is important:

- Terrain characteristics of a road like potholes, gravel road, speed bumps are very essential for a driver. Even more important is the fact that the driver needs to know this information in real-time. For example, if a car is travelling above speed limit, and there is a speed bump 300 meters ahead, then it is very critical for the driver to know this as soon as possible lest it might lead to a catastrophe.
- It can be used to monitor the wear and tear of wheels. It can also detect and report any possible vehicular breakdowns in advance. 

### Description
Real time estimation and visualisation of road terrain on web based map services like Google Maps.

## Approach
In this project, we have designed a system that collects terrain information of the roads using the sensors present in vehicles and stores it in a central database in real time. This information can then be visualised on a web-based map application like Google Maps to get the current terrain status of a route.

This is a data-driven approach in the sense that more the data we collect from the vehicles on road higher will be the accuracy with which we can project terrain information on the map application. 

## Implementation
<img src = "https://github.com/thedatamonk/RTOS-Project/blob/master/images/system_architecture.png">

In our setup, we have used 2 RPi each fitted with an accelerometer sensor. One of them is also fitted with a GPS sensor to collect the current location of the vehicle. These RPis are attached to either end (front and rear) of the vehicle. The one with the GPS is attached in the front end of the vehicle. 

We also designed a setup that used 4 RPis each with one accelerometer and fitted on each tyre.The GPS sensor in this setting is present in the center of the vehicle.This setup we believe will not only give more precise location of the potholes and speed bumps but also would give a decent estimate of the shape and size of the potholes. However, in this project we have only implemented the setup with 2 RPis and leave the second setup for future work.  

We have used the concepts of socket programming to read data from sensors and send it to the database. The polling of sensors is done every 1 second. In other words, the sensor data is send and stored in the database every 1 second. After having sufficient data, we wrote code to query the data from the database and visualise it on the different plots.

## Tools and technologies

### Hardware tools

**Rapberry Pi (rapbian OS) X2**: is built on a single circuit board with microprocessor, memory, I/O and other features primarily for educational purposes. Operating System used is Raspbian OS (Linux Distribution).

**Wifi dongle**: For pi2, we used wifi dongle to connect with mobile broadband(4G).

**Soldering equipment**: Soldering equipments were used to permanently glue sensors to the jumper wires.

**ADXL345 accelerometer X2**: It is a small, low power, 3-axis accelerometer with 13 bit resolution that measures the dynamic acceleration due to motion. Digital output data is accessible through either I2C or SPI digital interface.

**GPS module**: GPS module is used to detect the Latitude and Longitude of any location with exact time. It sends data related to tracking position in real time in NMEA format.


### Software tools

**InfluxDB**: It is an open source database optimized for fast, high-availability storage and retrieval of time series data. In our case, all the sensor data is stored in InfluxDB in real time. ***...--->(Please clarify this: in the cloud? Or PC?)***

**Grafana Labs**: It is an analytics tool that allows to query, visualize and understand any metrics from the stored data. In our case, we used Grafana to plot the time-series data and the geolocation of the anomalies in time-series data from InfluxDB in the inbuilt mapping tool for visualization.

## Issues
- System is not completely real time in the sense that a driver may not get terrain information immediately when an anomaly is encountered.
- Speed of vehicles should not very high else we won’t be able to poll the sensor data correctly.
- More the number of sensor, more difficult it is to sync data from all of them.***Please clarify if this point is valid or not***

## Conclusion and future work
In this project, we designed and implemented a working prototype of a system that can collect terrain data from the sensors fitted in the vehicle and store it in cloud in real-time. We also wrote scripts to read this data from **InfluxDB** and pre-processed it before visualising the potholes/speedbumps locations in **Grafana**.

As a part of our future work, we aim to make the visualisation component also real-time. We also aim to build systems with more sensors and compare their performance with that of our current system. 

