*****************************************
Connecting to a GPS Receiver Input Signal
*****************************************

.. contents:: Contents
    :local:

**THIS IS A PLACEHOLDER PAGE**

External GPS receiver signals provide a way for the system to acquire knowledge of the system position
and velocity in the Earth's reference frame.  This page serves as a placeholder for the description of
the connection to the GPS receiver.  In addition to connecting to the receiver, the unit needs to know
what format the input signal will be (for example, NMEA or NovAtel) and what the message will be (GGA
vs VTG, etc.).


Connecting a GPS Receiver
=========================

To connect the system to an external GPS receiver, the first step is to connect the TX and RX lines
to the appropriate pins for the device being used:

    1. OpenIMU300ZI: Pins 17 and 19 serve as the GPS input pins (`OpenIMU300ZI Connector Pinout <../300ZI/pinout.html#connector-pinout-including-gps-sensor-interface>`__)
    2. OpenIMU330BI: Pin X and Y serve as the GPS input pins (`OpenIMU330BI Connector Pinout <../330BI/pinout.html#openimu330bi-unit-package-pinout>`__)
    3. OpenIMU300RI: No pin available for connection to GPS receiver


Configuration Settings
======================

The second step in connecting to a GPS receiver is to configure the firmware to use the
signals.  An ideal place to perform this task is during 
initialization of the user-generated algorithm, commonly executed in *dataProcessingAndPresentation.c*.


Post-Connection Operations
===============================

Once the system is configured to accept and decode the GPS receiver input, ...


  1. *Function1()*
  2. *Function2()*


        
        
        