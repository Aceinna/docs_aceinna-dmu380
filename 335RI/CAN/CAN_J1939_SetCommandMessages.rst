CAN J1939 Set Request Messages
*******************************

.. contents:: Contents
    :local:

.. toctree::
    :maxdepth: 1

**Set Commands**


The following Set requests have been implemented in J1939 based application examples.
Users can modify provided requests and/or implement their own unique commands.

.. table::  *Set Commands*
    :align: left

    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    || **Request**              || **PGN**     || **PGN**|| **PF** || **PS**|| **Payload** || **Purpose**                            |
    ||                          || (dec)       || (hex)  || (dec)  || (dec) || **Length**  ||                                        |
    ||                          ||             ||        ||        ||       || (bytes)     ||                                        |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    ||  Reset Algorithm         ||  65360      ||  FF50  ||  255   || 80    ||  3          ||  Reset algorithm to initial conditions |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    || Set Packet Rate Divider  || 65365       || FF55   || 255    || 85    || 2           || Set rate dividers to increase/decrease |
    ||                          ||             ||        ||        ||       ||             || rate packets are set                   |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    || Set Data Packet Type(s)  || 65366       || FF56   || 255    || 86    || 2           || Select packet types to be sent         |
    ||                          ||             ||        ||        ||       ||             || periodically                           |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    ||   Set Digital Filters    || 65367       || FF57   || 255    || 87    ||  3          ||  Set LPF cutoff frequency for rate     |
    ||   Cutoff Frequencies     ||             ||        ||        ||       ||             ||  sensors and accelerometers            |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    || Set Orientation          ||  65368      ||  FF58  ||  255   || 88    ||  3          ||  Set unit orientation                  |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    || Set Unit Behavior        ||  65369      ||  FF59  ||  255   || 89    ||  4          ||  Set unit behavior                     |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    ||   Set Bank of PS         ||  65520      ||  FFF0  ||  255   || 240   ||  8          || Reconfigure PS numbers for set         |
    ||   Numbers for Bank0      ||             ||        ||        ||       ||             || requests                               |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    ||   Set Bank of PS         || 65521       || FFF1   || 255    || 241   ||  8          || Reconfigure PS numbers for set         |
    ||   Numbers for Bank1      ||             ||        ||        ||       ||             || requests                               |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
    || Save Configuration       || 65361       ||  FF51  || 255    || 81    ||  3          ||  Save all configuration                |
    ||                          ||             ||        ||        ||       ||             ||  data to non-volatile memory           |
    +---------------------------+--------------+---------+---------+--------+--------------+-----------------------------------------+
                                                 
.. note::

    PS values for all but the "Set Bank of PS Numbers for Bank0/Bank1" Set Commands can be changed by
    the the commands "Set Bank of PS Numbers" (see below). Updated values can be saved in nonvolatile memory and will be active upon
    following system restart/power-up. Provided in the table PS values are default values.

Payload for Set Messages
--------------------------

**Reset Algorithm**

    The following table provides the descriptions of the payload fields of the
    command and response messages.

    .. table::  *Reset Algorithm Request/Response Payload Fields*
        :align: left

        +----------+---------------------------------------------+
        || **Byte**|| **Description/Values**                     |
        +----------+---------------------------------------------+
        || 0       || Type: 0 = Request, 1 = Response, 2 = Reset |
        +----------+---------------------------------------------+
        || 1       || Destination Address                        |
        +----------+---------------------------------------------+
        || 2       || Response: 0 = Fail, 1 = Succeed            |
        +----------+---------------------------------------------+
		
	
**Set Packet Rate Divider**

    The following table provides the values of the packet rate divider response payload

    .. table::  Set *Packet Rate Divider Request/Response Payload Fields*
        :align: left

        +----------+-----------------+----------------------------------+
        || **Byte**|| **Description**|| **Byte Value**                  |
        +----------+-----------------+----------------------------------+
        || 0       || Destination    || Unique                          |
        ||         || Address        ||                                 |
        +----------+-----------------+----------------------------------+
        || 1       ||                || **Byte Value** -                |
        |          ||                | **Packet Broadcast Rate (Hz)**   |
        |          ||                || 0  - Quiet Mode - no broadcast  |
        |          || Packet         || 1  - 100 (default)              |
        |          || Divider        || 2  - 50                         |
        |          || Value          || 4  - 25                         |
        |          ||                || 5  - 20                         |
        |          ||                || 10 (0x0a) - 10                  |
        |          ||                || 20 (0x14) -  5                  |
        |          ||                || 25 (0x19) -  4                  |
        |          ||                || 50 (0x32) -  2                  |
        +----------+-----------------+----------------+-----------------+


		
**Set Periodic Data Packet Type(s)**

    The following table provides the *Set Data Packet Type(s)* payload. Each bit in the request payload enables specific data packet for periodic transmission.
    Any combination of data packets can be chosen.

    .. table::  *Set Data Packet Type(s) Field*
        :align: left


        +----------+-----------------+-------------------------------+
        || **Byte**|| **Description**||  **Byte Value**              |
        +----------+-----------------+-------------------------------+
        || 0       || Destination    || Unique                       |
        |          || Address        ||                              |
        +----------+-----------------+-------------------------------+
        || 1       || Selected Data  || Data Packet Type(s) Bitmask: |
        |          || Packet Type(s) || Bit 0 - SSI2                 |
        |          || Bitmask (LSB)  || Bit 1 - Angular Rate         |
        |          ||                || Bit 2 - Acceleration         |
        |          ||                || Bit 3 - HR Angular Rate      |
        |          ||                || Bit 4 - HR Acceleration      |
        +----------+-----------------+-------------------------------+
        || 2       || Selected Data  ||  Reserved                    |
        |          || Packet Type(s) ||                              |
        |          || Bitmask (MSB)  ||                              |
        +----------+-----------------+-------------------------------+
		
		
		
		
**Set Digital Filter Cutoff Frequencies**

    The following table provides descriptions of the request payload

    .. table::  *Digital Filter Cutoff Frequencies Request Payload*
        :align: left

        +--------------+------------------------------+----------------------------+
        || **Payload** || **Description/Values**      || **Values**                |
        || **Byte**    ||                             ||                           |
        +--------------+------------------------------+----------------------------+
        || 0           || Destination Address         || Unique                    |
        +--------------+------------------------------+----------------------------+
        || 1           || Cutoff Frequencies (Hz) for ||                           |
        ||             || Angular Rate Sensors        || 0, 2, 5, 10, 25, 40, or 50|
        +--------------+------------------------------+----------------------------+
        || 2           || Cutoff Frequencies (Hz) for ||                           |
        ||             || Accelerometer Sensors       || 0, 2, 5, 10, 25, 40, or 50|
        +--------------+------------------------------+----------------------------+
		
		
		
		

**Set Orientation**

    The following table shows the payload layout

    .. table:: *Set Orientation Payload Layout*
        :align: left

        +----------+-------------------------+-------------------+
        || **Byte**|| **Meaning**            || **Value**        |
        +----------+-------------------------+-------------------+
        || 0       || Destination Address    || Unique           |
        +----------+-------------------------+-------------------+
        || 1       || Orientation Value (MSB)||  see table below |
        +----------+-------------------------+-------------------+
        || 2       || Orientation VAlue (LSB)||  see table below |
        +----------+-------------------------+-------------------+

    The following table provides the orientation values and meanings:

    .. table:: *Set Orientation Field Descriptions*
        :align: left

        +------------------+-----------------------+
        || **Orientation** || **X/Y/Z Axis**       |
        || **Value**       ||                      |
        +------------------+-----------------------+
        || 0x0000          || +Ux +Uy +Uz (default)|
        +------------------+-----------------------+
        || 0x0009          || -Ux -Uy +Uz          |
        +------------------+-----------------------+
        || 0x0023          || -Uy +Ux +Uz          |
        +------------------+-----------------------+
        || 0x002A          || +Uy -Ux +Uz          |
        +------------------+-----------------------+
        || 0x0041          || -Ux +Uy -Uz          |
        +------------------+-----------------------+
        || 0x0048          || +Ux -Uy -Uz          |
        +------------------+-----------------------+
        || 0x0062          || +Uy +Ux -Uz          |
        +------------------+-----------------------+
        || 0x006B          || -Uy -Ux -Uz          |
        +------------------+-----------------------+
        || 0x0085          || -Uz +Uy +Ux          |
        +------------------+-----------------------+
        || 0x008C          || +Uz -Uy +Ux          |
        +------------------+-----------------------+
        || 0x0092          || +Uy +Uz +Ux          |
        +------------------+-----------------------+
        || 0x009B          || -Uy -Uz +Ux          |
        +------------------+-----------------------+
        || 0x00C4          || +Uz +Uy -Ux          |
        +------------------+-----------------------+
        || 0x00CD          || -Uz -Uy -Ux          |
        +------------------+-----------------------+
        || 0x00D3          || -Uy +Uz -Ux          |
        +------------------+-----------------------+
        || 0x00DA          || +Uy -Uz -Ux          |
        +------------------+-----------------------+
        || 0x0111          || -Ux +Uz +Uy          |
        +------------------+-----------------------+
        || 0x0118          || +Ux -Uz +Uy          |
        +------------------+-----------------------+
        || 0x0124          || +Uz +Ux +Uy          |
        +------------------+-----------------------+
        || 0x012D          || -Uz -Ux +Uy          |
        +------------------+-----------------------+
        || 0x0150          || +Ux +Uz -Uy          |
        +------------------+-----------------------+
        || 0x0159          || -Ux -Uz -Uy          |
        +------------------+-----------------------+
        || 0x0165          || -Uz +Ux -Uy          |
        +------------------+-----------------------+
        || 0x016C          || +Uz -Ux -Uy          |
        +------------------+-----------------------+



**Set Unit Behavior**

	The first payload byte is destination address. 
	The next payload byte used to enable/disable specific types of unit behavior. To affect a specific behavior type, set the corresponding bit to 1. Any combination of behaviors can be selected. Unit behavior settings can be permanently saved. See Table 9. Unit behavior payload.

    .. table:: *Set Unit Behavior*
        :align: left

        +----------+-------------------------------------------------------------+
        || **Byte**|| **Selected Unit Behavior type**                            |
        +----------+-------------------------------------------------------------+
        || 0       || DA                                                         |
        +----------+-------------------------------------------------------------+
        || 1       || Enable behavior bitmask:                                   |
        ||         || Bit 0 – Restart on Over range (default = OFF)              |        
        ||         || Bit 1 – Reserved                                           |
        ||         || Bit 2 – Send uncorrected rates in Angular Rates            |
        ||         ||         (ARI) message (default = OFF)                      |
        ||         || Bit 3 = Swap sequence of axes from XYZ to YXZ in all       |
        ||         || angular rates and acceleration Messages. Affects HR        |
        ||         || messages as well (default = OFF)                           |
        ||         || Bit 4 – Enable Automatic Baud-rate Detection (default = ON)|
        ||         || Bit 5 - Convert accelerometers frame from NED to NWU       |
        ||         || (swap signs in Y and Z axes). Affects HR ACC message as    |
        ||         || well (default = OFF)                                       |
        ||         || Bit 6 -  Enable User VG Algorithm (default = ON)           |
        ||         || Bit 7 – Reserved                                           |
        +----------+-------------------------------------------------------------+





**Set Bank of PS Numbers**


	Users may change the default PS numbers inside OPENIMU335 if the pre-configured values have already 
	been used in their system. PS numbers include hardware bit, software bit, status, packet rate etc. 
	The two commands below are issued by user’s ECU and sent to OPENIMU335, which will change the 
	corresponding PS values. Tables below shows the format of these two commands. 
	
	OPENIMU335 will decode the two incoming packets and switch the default PS numbers to the values assigned by users. 
	The new PS numbers will take effect immediately and but also can be saved in non-volatile memory by the 
	command “Configuration Save” and will retain their values after powering cycle.
    
	The Bank0 payload contains 8 bytes, and each of the bytes is the newly assigned PS number to Get or Set commands. 
	The values at byte 1, 5 are new PS numbers of algorithm reset status request. The remaining bytes are reserved.
	
	The following tables provide descriptions of the payload for Bank0 and Bank1 set commands

    .. table:: *Set Bank of PS Numbers for Bank0 Payload*
        :align: left

        +----------+-------------------------------+
        || **Byte**|| **Parameters**               |
        +----------+-------------------------------+
        || 0       || Destination Address (DA)     |
        +----------+-------------------------------+
        || 1       || New PS for algorithm         |
        ||         || reset command (default 80)   |
        +----------+-------------------------------+
        || 2       || Reserved                     |
        +----------+-------------------------------+
        || 3       || Reserved                     |
        +----------+-------------------------------+
        || 4       || Reserved                     |
        +----------+-------------------------------+
        || 5       || New PS for status            |
        ||         || request command (default 84) |
        +----------+-------------------------------+
        || 6       || Reserved                     |
        +----------+-------------------------------+
        || 7       || Reserved                     |
        +----------+-------------------------------+
    
    |	
	The Bank1 payload contains 8 bytes, and each of the bytes is the newly assigned PS number to set command. 
	The values of bytes 1, 2, 3, 4, 5 are the new PS numbers of packet rate, packet type, digital filter, orientation 
	and user behavior. The remaining bytes, 5-7, are reserved.
	
    .. table::  *Set Bank of PS Numbers for Bank1 Payload*
        :align: left

        +----------+------------------------------------------------+
        || **Byte**|| **Parameters**                                |
        +----------+------------------------------------------------+
        || 0       || Destination Address (DA)                      |
        +----------+------------------------------------------------+
        || 1       || New PS for packet rate                        |
        ||         || command/request (default 85)                  |
        +----------+------------------------------------------------+
        || 2       || New PS for packet type                        |
        ||         || command/request (default 86)                  |
        +----------+------------------------------------------------+
        || 3       || New PS for digital filters                    |
        ||         || command/request (default 87)                  |
        +----------+------------------------------------------------+
        || 4       || New PS for orientation                        |
        ||         || command/request   (default 88)                |
        +----------+------------------------------------------------+
        || 5       || New PS for unit behavior                      |
        ||         || command/request (default 89)                  |
        +----------+------------------------------------------------+
        || 6       || Reserved                                      |
        +----------+------------------------------------------------+
        || 7       || Reserved                                      |
        +----------+------------------------------------------------+


.. note:: PS values in these commands can be chosen within range 64 - 127.

.. note:: User can restore default PS values by sending all zeroes in payload of these commands. Then issue “Configuration save” command and recycle power or send “Algorithm reset” command with active reset option.


**Save Configuration**

    The next table provides the descriptions of the payload fields of the
    command and response messages.

    .. table::  *Save Configuration Request/Response Payload Fields*
        :align: left

        +----------+---------------------------------------------+
        || **Byte**|| **Description/Values**                     |
        +----------+---------------------------------------------+
        || 0       || Type: 0 = Request, 1 = Response, 2 = Reset |
        +----------+---------------------------------------------+
        || 1       || Destination Address                        |
        +----------+---------------------------------------------+
        || 2       || Response: 0 = Fail, 1 = Succeed            |
        +----------+---------------------------------------------+


		

































