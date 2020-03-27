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

`CAN J1939 Messaging & Example Application <https://openimu.readthedocs.io/en/latest/software/CAN/CAN_J1939_Application.html>`__