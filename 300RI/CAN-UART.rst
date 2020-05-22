CAN and UART
============

.. contents:: Contents
    :local:

Ports
----------------

The OpenIMU300RI has two external ports; one UART port and one CAN bus port.
Based on these available external ports, the OpenIMU300RI can be configured
in several modes for communication with the external world.

The usage modes are:

+---------------------+-------------------------------------------+
| **UART Mode**       | - Typically used during early development |
|                     | - Single UART for all messages,           |
|                     |   debug output, and firmware update       |
+---------------------+-------------------------------------------+
| **CAN + UART Mode** | - Typically used during late development  |
|                     | - Uses CAN Port for messages and          |
|                     |   firmware update                         |
|                     | - Single UART for all messages,           |
|                     |   debug output, and firmware update       |
+---------------------+-------------------------------------------+
| **CAN Mode**        | - Typically used for production           |
|                     | - Uses CAN Port for messages and          |
|                     |   firmware update                         |
+---------------------+-------------------------------------------+

CAN Messaging
----------------

To learn about CAN J1939 Messaging & Example Application For OpenIMU330RI, please see the following
page: 

1. `CAN J1939 Messaging & Example Application <../software/CAN/CAN_J1939_Application.html#CAN J1939 Messaging>`__


UART Messaging
----------------

To learn more about the OpenIMU UART Messaging Framework, please see the following pages: 

1. `UART Messsaging Framework <../software/UARTmessaging.html#OpenIMU UART Messaging Framework>`__