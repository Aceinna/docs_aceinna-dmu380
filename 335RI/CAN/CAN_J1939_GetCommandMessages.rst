CAN J1939 Get Request Messages
*******************************

.. contents:: Contents
    :local:

.. toctree::
    :maxdepth: 1


  
In table below provided list of the parameters which can be requested from ECU, including their PF, PS and payload length of response messages


.. table::  *List of ECU parameters available for Requests*
    :align: left

    +-------------------------------+-------------+--------------+-------------+--------------+
    ||  **Parameter**               || **PGN**    ||   **PF**    ||  **PS**    || **Payload** |
    ||                              || (dec)      ||   (dec)     ||  (dec)     || **Length**  |
    ||                              ||            ||             ||  (See note)|| (bytes)     |
    +-------------------------------+-------------+--------------+-------------+--------------+
    || Firmware  Version            || 65242      ||  254        || 218        || 5           |
    +-------------------------------+-------------+--------------+-------------+--------------+
    ||  ECU ID                      || 64965      ||  253        || 197        || 8           |
    +-------------------------------+-------------+--------------+-------------+--------------+
    ||  Packet Rate                 || 65365      ||  255        || 85         || 2           |
    +-------------------------------+-------------+--------------+-------------+--------------+
    ||  Packet Type                 || 65366      ||  255        || 86         || 2           |
    +-------------------------------+-------------+--------------+-------------+--------------+
    ||  LPF Cutoff Frequency        || 65367      ||  255        || 87         || 3           |
    +-------------------------------+-------------+--------------+-------------+--------------+
    ||  Orientation                 || 65368      ||  255        || 88         || 3           |
    +-------------------------------+-------------+--------------+-------------+--------------+
    ||  Master BIT status word      || 65364      ||  254        || 84         || 2           |
    +-------------------------------+-------------+--------------+-------------+--------------+
    ||  Unit Behavior               || 65369      ||  255        || 89         || 2           |
    +-------------------------------+-------------+--------------+-------------+--------------+
	
	
.. note::

    *   Provided PS values for all but the *Get Software Version* and *Get ECU ID* can be changed by the
        "Set Bank of PS Numbers for Bank1" command.  The given values are the default values.
    *   In responses values of PF and PS field in extended headers have the same PF+PS values as requested.

Payload for Get Messages
--------------------------
The following table describe the payloads for responses to Get Requests


.. table::    *Firmware Version Response Payload*
    :align: left

    +-----------+-----------------------+
    || **Byte** || **Description**      |
    +-----------+-----------------------+
    || 0        || Major Version Number |
    +-----------+-----------------------+
    || 1        || Minor Version Number |
    +-----------+-----------------------+
    || 2        || Patch Number         |
    +-----------+-----------------------+
    || 3        || Stage Number         |
    +-----------+-----------------------+
    || 4        || Build Number         |
    +-----------+-----------------------+

.. table::    *ECU ID 64 Bit Response Payload*
    :align: left

    +--------------+-------------------------+
    ||  **Bits**   ||  **Contents**          |
    +--------------+-------------------------+
    ||  bits 0     || Arbitrary Address      |
    ||  bit  1:3   || Industry Group         |
    ||  bit  4:7   || Vehicle System Instance|
    ||  bits 8:14  || System Bits            |
    ||  bits 15    || Reserved               |
    ||  bits 16:23 || Function Bits          |
    ||  bits 24:28 || Function Instance      |
    ||  bits 29:31 || ECU Bits               |
    ||  bits 32:42 || Manufacturer code      |
    ||  bits 43:63 || ID bits                |
    +--------------+-------------------------+

.. table::  *Packet Rate Response Payload*

    +-----------+-----------------------+
    || **Byte** || **Description**      |
    +-----------+-----------------------+
    || 0        || Source Address       |
    +-----------+-----------------------+
    || 1        || Output Data Rate     |
    +-----------+-----------------------+

.. table::  *Packet Type Response Payload*

    +-----------+----------------------------+
    || **Byte** || **Description**           |
    +-----------+----------------------------+
    || 0        || Source Address            |
    +-----------+----------------------------+
    || 1        || Packet Types Bitmask (LSB)|
    +-----------+----------------------------+
    || 2        || Packet Types Bitmask (MSB)|
    +-----------+----------------------------+


.. table:: *Digital Cutoff Frequency Response Payload*

    +-----------+-----------------------+
    || **Byte** || **Description**      |
    +-----------+-----------------------+
    || 0        || Source Address       |
    +-----------+-----------------------+
    || 1        || Angular Rate Cutoff  |
    +-----------+-----------------------+
    || 2        || Acceleration Cutoff  |
    +-----------+-----------------------+

.. table:: *Orientation Response Payload*

    +-----------+----------------------------------+
    || **Byte** || **Description**                 |
    +-----------+----------------------------------+
    || 0        || Source Address                  |
    +-----------+----------------------------------+
    || 1        || Orientation Value (MSB)         |
    +-----------+----------------------------------+
    || 2        || Orientation Value (LSB)         |
    +-----------+----------------------------------+


.. table::    *Master Bit Status Word*
    :align: left

    +--------------+-------------------------+------------------------------------------------------------------+
    ||  **Bits**   ||   **Contents**         ||                   **Description**                               |
    +--------------+-------------------------+------------------------------------------------------------------+
    ||  bit  0     || Master Status          || 0 = normal, 1 = hardware, sensor, CAN, or software alert/error  |
    ||  bit  1     || Hardware Status        || 0 = normal, 1 = hardware alert/error                            |
    ||  bit  2     || Software Status        || 0 = normal, 1 = software alert/error                            |
    ||  bit  3     || Sensor Status          || 0 = normal, 1 = sensors alert/error                             |
    ||  bit  4     || Reserved               ||								        |
    ||  bit  5     || Reserved               ||                                                                 |
    ||  bit  6     || Reserved               ||                                                                 |
    ||  bit  7     || Reserved               ||                                                                 |
    ||  bit  8     || Algorithm Init         || 0 = normal, 1 = algorithm in initialization mode                |
    ||  bit  9     || High Gain              || 0 = algorithm in low gain mode, 1 = algorithm in high gain mode |               
    ||  bit  10    || Attitude only Algorithm|| 0 = navigation state tracking, 1 = attitude only state tracking |
    ||  bit  11    || Reserved               || 								|
    ||  bit  12    || Sensor Over Range      || 0 = not asserted, 1 = asserted                                  |
    ||  bits 13:15 || Reserved               || 								|
    +--------------+-------------------------+------------------------------------------------------------------+


.. note::

    *   For Orientation, Cutoff Frequencies Packet Type and Packet Rate responses values of parameters will be the same as in the set commands for these parameters.
