SPI and UART
============

.. contents:: Contents
    :local:
	
Ports
-------	

The OpenIMU300ZI can be configured in a number of ways for communication with external world.  There are up to three external UART ports and one external SPI port.

Typical configurations include:

+-------------------------+-----------------------------------------+
| **3 UART Mode**         | - User UART                             |
|                         | - GPS/External Sensor UART              |
|                         | - Debug UART                            |
+-------------------------+-----------------------------------------+
| **UART + SPI Mode**     |  - User SPI Port                        |
|                         |  - GPS/Debug UART                       |
+-------------------------+-----------------------------------------+


SPI & UART Messaging
---------------------

To learn more about the OpenIMU SPI & UART Messaging Framework, please see the following pages: 

1. `SPI Messaging Framework <https://openimu.readthedocs.io/en/latest/software/SPImessaging.html>`__
2. `UART Messsaging Framework <https://openimu.readthedocs.io/en/latest/software/UARTmessaging.html>`__