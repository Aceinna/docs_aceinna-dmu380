*****************************************
Synchronization to External Clock Signals
*****************************************

.. contents:: Contents
    :local:

External clock signals provide a way for the system to synchronize sensor sampling and processing, as
well as algorithm operations, to an external source.  In general, this can improve the performance of
inertial systems and algorithms by enhancing the time-relevancy measurement of the sensor output, via
a highly accurate timestamp with micro-second resolution, or by enabling algorithm updates with
information that is more timely.

By default the system is configured to synchronize to a 1 kHz signal; all that is required is to
connect the signal to the OpenIMU device.  However, to enable synchronization lock to an external 1 Hz
signal (such as the GPS PPS signal) the user must configure the firmware to operate with a 1 Hz
external clock by calling *platformEnableGpsPps(TRUE);* during system initialization.


Connecting an External Clock
============================

To synchronize the system to an external clock, the first step is to connect the signal to the 
appropriate pin for the device being used:

    1. OpenIMU300ZI: Pin 2 serves as the clock input (`OpenIMU300ZI Connector Pinout <../300ZI/pinout.html#connector-pinout-including-gps-sensor-interface>`__)
    2. OpenIMU330BI: Pin J3 serves as the clock input (`OpenIMU330BI Connector Pinout <../330BI/pinout.html#openimu330bi-unit-package-pinout>`__)
    3. OpenIMU300RI: No pin available for synchronization to external clock


Configuration Settings
======================

The second step in synchronizing to an external clock signal is to configure the firmware to use the
external signal connected to the external clock pint.  As mentioned above, the system is automatically
configured to use a 1 kHz.  To connect and synchronize to a 1 Hz signal, the user must configure the
firmware by calling *platformEnableGpsPps(TRUE);*.  An ideal place to perform this task is during 
initialization of the user-generated algorithm, commonly executed in *dataProcessingAndPresentation.c*.

The following code snippet shows how the INS application initializes the system to synchronize to the
1 PPS signal: ::

    // Next function is common for all platforms, but implementation of the methods inside is
    // platform-dependent.  Call to this function is made from DataAcquisitionTask during the
    // initialization phase.  All user algorithm and data structures should be initialized
    // here, if used.
    void initUserDataProcessingEngine()
    {
        InitUserAlgorithm();         // default implementation located in file user_algorithm.c
        platformEnableGpsPps(TRUE);  // Init PPS sync engine 
    }


Post-Synchronization Operations
===============================

Once the system is configured to synchronize to the expected input clock signal, there are a variety
of functions available to take advantage of the synchronization.  Two such functions are:

  1. *platformGetSolutionTstampAsDouble()*
  2. *platformGetEstimatedITOW()*

Additionally, users can take advantage of the PPS synchronization by monitoring for, and responding to,
the PPS signal using the function *platformGetPpsFlag(TRUE);*, where TRUE indicates that the PPS flag
is reset after reading.

The time delay between the PPS signal and the availability of the GPS data can be measured using the
function *getSystemTime()*.  This measurement can then be used to account for by the delay in the
algorithm.
        
        
        