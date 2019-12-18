**********************************
Connecting to an External Odometer
**********************************

.. contents:: Contents
    :local:

**THIS IS A PLACEHOLDER PAGE**

External odometer signals provide a way for the system to acquire knowledge of the system velocity and
heading relative to the vehicle-frame.  This page serves as a placeholder for the description of
the connection to the odometer.  In addition to connecting to the odometer, the unit needs to know
what format the input signal will be and what the message will be.


Connecting an Odometer
======================

To connect the system to a non CAN-based, external odometer, the first step is to connect the signal lines
to the appropriate pins for the device being used:

    1. OpenIMU300ZI: Pins X and Y serve as the input pins (`OpenIMU300ZI Connector Pinout <../300ZI/pinout.html#connector-pinout-including-gps-sensor-interface>`__)
    2. OpenIMU330BI: Pin X and Y serve as the input pins (`OpenIMU330BI Connector Pinout <../330BI/pinout.html#openimu330bi-unit-package-pinout>`__)
    3. OpenIMU300RI: No pin available for connection to odometer


Configuration Settings
======================

The second step in connecting to an odometer is to configure the firmware to use the signals.  An ideal
place to perform this task is during initialization of the user-generated algorithm, commonly executed
in *dataProcessingAndPresentation.c*.


Post-Connection Operations
===============================

Once the system is configured to accept and decode the odometer input, ...


  1. *Function1()*
  2. *Function2()*



