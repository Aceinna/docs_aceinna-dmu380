*******************************************
OpenIMU Hardware/Software Interface 
*******************************************

.. contents:: Contents
    :local:

This section describes firmware-configurable connections from external hardware to the OpenIMU platform.  In particular, 
it describes how external connections are connected and how the platform code modules are inputs and work together.  If
the platform cannot support the connection (such as the OpenIMU300RI( then this section is not applicable.  Examples of
external sources include:

    *   `Synchronization to external clock signals <hw_sw_interface/synchronization.html#synchronization-to-external-clock-signals>`__
    *   `GPS receiver input <hw_sw_interface/gps_input.html#gps-receiver-input-signal>`__
    *   `Odometer input <hw_sw_interface/odometer.html#connecting-to-an-external-odometer>`__

If the input is provided via a software interface, such as CAN, then this section is not applicable.

.. toctree::
    :maxdepth: 1
    :hidden:

    hw_sw_interface/synchronization
    hw_sw_interface/gps_input
    hw_sw_interface/odometer
