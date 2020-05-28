CAN J1939 Data Messages
***********************

.. contents:: Contents
    :local:

.. toctree::
    :maxdepth: 1


The following Data messages are implemented in the example applications.
The user can modify provided messages or add messages as needed.
The rate of data messages can be configured by SET commands.

.. table:: *Data Messages*
    :align: left

    +-------------------+--------------+--------+--------+----------+---------+-----------------+---------------------------------+
    || **Data Packet**  || **Priority**|| **PF**|| **PS**|| **PGN** || **PGN**|| **Data Length**||   **Purpose**                  |
    ||                  ||             || (dec) || (dec) || (dec)   || (Hex)  ||  (bytes)       ||                                |
    +-------------------+--------------+--------+--------+----------+---------+-----------------+---------------------------------+
    ||   Slope Sensor   ||   3         || 240   || 41    || 61481   ||  F029  ||  8             || Provide pitch & roll angles    |
    ||   Information    ||             ||       ||       ||         ||        ||                || with Standard J1939 Resolution |
    ||   Type 2         ||             ||       ||       ||         ||        |                 ||                                |
    +-------------------+--------------+--------+--------+----------+---------+-----------------+---------------------------------+
    ||  Angular Rate    ||   3         || 240   || 42    || 61482   ||  F02A  ||  8             || Provide Angular Rates for      |
    ||  Sensor Data     ||             ||       ||       ||         ||        ||                || roll, pitch and yaw            |
    ||                  ||             ||       ||       ||         ||        ||                || with Standard J1939 Resolution |
    +-------------------+--------------+--------+--------+----------+---------+-----------------+---------------------------------+
    ||  Acceleration    ||   2         || 240   || 45    || 61485   ||  F02D  ||  8             || Provide X, Y,& Z acceleration  |
    ||  Sensor Data     ||             ||       ||       ||         ||        ||                || with Standard J1939 Resolution |
    +-------------------+--------------+--------+--------+----------+---------+-----------------+---------------------------------+
    ||  HR Angular Rate ||   3         || 255   || 107   || 65387   ||  FF6B  ||  8             || Non standard message with      |
    ||  Sensor Data     ||             ||       ||       ||         ||        ||                || higher resolution than         |
    ||                  ||             ||       ||       ||         ||        ||                || Standard J1939 Resolution      |
    +-------------------+--------------+--------+--------+----------+---------+-----------------+---------------------------------+
    ||  HR Acceleration ||   2         || 255   || 108   || 65388   ||  FF6C  ||  8             || Non standard message with      |
    ||  Sensor Data     ||             ||       ||       ||         ||        ||                || higher resolution than         |
    ||                  ||             ||       ||       ||         ||        ||                || Standard J1939 Resolution      |
    +-------------------+--------------+--------+--------+----------+---------+-----------------+---------------------------------+
	

Data Packet Description
--------------------------
	
**Slope Sensor Information - Type 2 (SSI2) Data Packet**


The following table describes the SSI2 Data Packet Payload:

.. table:: *SSI2 Data Packet Payload*
    :align: left

    +------------+----------------+------------------+-----------------+------------+
    || **Bytes** || **Field Name**|| **Range**       || **Resolution** || **Offset**|
    +------------+----------------+------------------+-----------------+------------+
    || 0:2       || Pitch         || -250 to +252 deg|| 1/32768 deg/bit|| -250 deg  |
    +------------+----------------+------------------+-----------------+------------+
    || 3:5       || Roll          || -250 to +252 deg|| 1/32768 deg/bit|| -250 deg  |
    +------------+----------------+------------------+-----------------+------------+
    || 6:7       || FoM,Latency   || Ignore          || Ignore         || Ignore    |
    +------------+----------------+------------------+-----------------+------------+

|
	
**Angular Rate Information (ARI) Data Packet**


The following table describes the Angular Rate Data Packet:

.. table:: *Angular Rate Information (ARI) Data Packet Payload*
    :align: left

    +-----------------+----------------+------------------------+----------------------+------------+
    || **Byte Number**|| **Parameter** || **Range**             || **Resolution**      || **Offset**|
    +-----------------+----------------+------------------------+----------------------+------------+
    || 0:1            || Angular Rate X|| -250 to +250.992 deg/s|| 1/128 deg/second/bit|| -250 deg  |
    +-----------------+----------------+------------------------+----------------------+------------+
    || 2:3            || Angular Rate Y|| -250 to +250.992 deg/s|| 1/128 deg/second/bit|| -250 deg  |
    +-----------------+----------------+------------------------+----------------------+------------+
    || 4:5            || Angular Rate Z|| -250 to +250.992 deg/s|| 1/128 deg/second/bit|| -250 deg  |
    +-----------------+----------------+------------------------+----------------------+------------+
    || FoM,Latency    || FoM,Latency   || Ignore                || Ignore              || Ignore    |
    +-----------------+----------------+------------------------+----------------------+------------+



.. note:: By default, the Aceinna Angular rate packet is arranged in the order X, then Y, then Z rate, which is different from the J1939 standard due to legacy compatibility reasons. J1939 defines the message order as Y, then X, then Z rate. Scaling and offsets are consistent with the standard. If desired, it’s possible to switch to the J1939 message sequence (see “Configuring Unit Behavior”, PGN65369 below).

.. note:: By default, the Aceinna Angular rate packet will provide angular rates corrected for bias by the internal EKF algorithm. It is possible to disable this correction  (see “Configuring Unit Behavior”, PGN65369 below), and output calibrated but uncorrected angular rates. This is recommended for systems where there is an external algorithm running, which is externally correcting angular rate bias.

|

**Acceleration Sensor (ACCS) Data Packet**

The following table describes the Acceleration Data Packet:

.. table:: *Acceleration Sensor (ACCS) Data Packet Payload*
    :align: left

    +------------+--------------------+-----------------------+-----------------+-------------+
    || **Byte**  ||  **Parameter**    || **Range**            || **Resolution** || **Offset** |
    || **Number**||                   ||                      ||                ||            |
    +------------+--------------------+-----------------------+-----------------+-------------+
    || 0:1       || Acceleration X    || -320 to 320.55 m/s**2|| 0.01 m/s**2/bit|| -320 m/s**2|
    +------------+--------------------+-----------------------+-----------------+-------------+
    || 2:3       || Acceleration Y    || -320 to 320.55 m/s**2|| 0.01 m/s**2/bit|| -320 m/s**2|
    +------------+--------------------+-----------------------+-----------------+-------------+
    || 4:5       || Acceleration Z    || -320 to 320.55 m/s**2|| 0.01 m/s**2/bit|| -320 m/s**2|
    +------------+--------------------+-----------------------+-----------------+-------------+
    || 6:7       || FoM,Latency       || Ignore               || Ignore         || Ignore     |
    +------------+--------------------+-----------------------+-----------------+-------------+


.. note:: By default, the Aceinna Acceleration packet is arranged as in the order X, then Y, then Z, which is different from the J1939 standard due to legacy compatibility reasons. J1939 defines the message order as Y, then X, then Z acceleration. Scaling and offsets are consistent with the standard. If desired, it’s possible to switch to the J1939 message sequence (see “Configuring Unit Behavior”, PGN65369 below).

.. note:: By default, the Aceinna Acceleration packet is defined in the context of a NED (North-East-Down) orientation, which is different from the J1939 standard due to legacy compatibility reasons. J1939 defines the acceleration orientation in a Z-up or “North-West-Up” orientation. Both ACEINNA and the J1939 standard define the ARI and SSI2 messages in the NED frame. If desired, it’s possible to switch to the J1939 message format (see “Configuring Unit Behavior”, PGN65369 below).

|
	
**HR Angular Rate Data Packet (custom)**


The following table describes the Angular Rate Data Packet:

.. table:: *HR Angular Rate Data Packet Payload*
    :align: left

    +------------------+------------------+------------------------+-----------------------+------------+
    || **BIT Position**|| **Parameter**   || **Range**             || **Resolution**       || **Offset**|
    +------------------+------------------+------------------------+-----------------------+------------+
    || 0:18            || Angular Rate X  || -250 to +250.992 deg/s|| 1/1024 deg/second/bit|| -250 deg/s|
    +------------------+------------------+------------------------+-----------------------+------------+
    || 19:37           || Angular Rate Y  || -250 to +250.992 deg/s|| 1/1024 deg/second/bit|| -250 deg/s|
    +------------------+------------------+------------------------+-----------------------+------------+
    || 38:56           || Angular Rate Z  || -250 to +250.992 deg/s|| 1/1024 deg/second/bit|| -250 deg/s|
    +------------------+------------------+------------------------+-----------------------+------------+
    || 57,58           || Lateral FoM     || N/A                   || N/A                  || N/A       |
    +------------------+------------------+------------------------+-----------------------+------------+
    || 59,60           || Longitudinal FoM|| N/A                   || N/A                  || N/A       |
    +------------------+------------------+------------------------+-----------------------+------------+
    || 61,62           || Vertical FoM    || N/A                   || N/A                  || N/A       |
    +------------------+------------------+------------------------+-----------------------+------------+

.. note:: By default, the Aceinna Angular rate packet is arranged in the order X, then Y, then Z rate, which is different from the J1939 standard due to legacy compatibility reasons. J1939 defines the message order as Y, then X, then Z rate. Scaling and offsets are consistent with the standard. If desired, it’s possible to switch to the J1939 message sequence (see “Configuring Unit Behavior”, PGN65369 below).

.. note:: By default, the Aceinna Angular rate packet will provide angular rates corrected for bias by the internal EKF algorithm. It is possible to disable this correction  (see “Configuring Unit Behavior”, PGN65369 below), and output calibrated but uncorrected angular rates. This is recommended for systems where there is an external algorithm running, which is externally correcting angular rate bias.


|

**HR Acceleration Sensor Data Packet (custom)**

The following table describes the Acceleration Data Packet:

.. table:: *HR Acceleration Sensor Data Packet Payload*
    :align: left

    +------------------+--------------------+-----------------------+---------------------+-------------+
    || **BIT Position**|| **Parameter**     || **Range**            || **Resolution**     || **Offset** |
    +------------------+--------------------+-----------------------+---------------------+-------------+
    || 0:18            || Acceleration X    || -320 to 321 m/s**2   || 0.00125  m/s**2/bit||  320 m/s**2|
    +------------------+--------------------+-----------------------+---------------------+-------------+
    || 19:37           || Acceleration Y    || -320 to 321 m/s**2   || 0.00125  m/s**2/bit||  320 m/s**2|
    +------------------+--------------------+-----------------------+---------------------+-------------+
    || 38:56           || Acceleration Z    || -320 to 321 m/s**2   || 0.00125  m/s**2/bit||  320 m/s**2|
    +------------------+--------------------+-----------------------+---------------------+-------------+
    || 57,58           || Lateral FoM       || N/A                  || N/A                || N/A        |
    +------------------+--------------------+-----------------------+---------------------+-------------+
    || 59,60           || Longitudinal FoM  || N/A                  || N/A                || N/A        |
    +------------------+--------------------+-----------------------+---------------------+-------------+
    || 61,62           || Vertical FoM      || N/A                  || N/A                || N/A        |
    +------------------+--------------------+-----------------------+---------------------+-------------+


.. note:: By default, the Aceinna Acceleration packet is arranged as in the order X, then Y, then Z, which is different from the J1939 standard due to legacy compatibility reasons. J1939 defines the message order as Y, then X, then Z acceleration. Scaling and offsets are consistent with the standard. If desired, it’s possible to switch to the J1939 message sequence (see “Configuring Unit Behavior”, PGN65369 below).

.. note:: By default, the Aceinna Acceleration packet is defined in the context of a NED (North-East-Down) orientation, which is different from the J1939 standard due to legacy compatibility reasons. J1939 defines the acceleration orientation in a Z-up or “North-West-Up” orientation. Both ACEINNA and the J1939 standard define the ARI and SSI2 messages in the NED frame. If desired, it’s possible to switch to the J1939 message format (see “Configuring Unit Behavior”, PGN65369 below).

.. note:: As with all multiple byte fields, the LSB of each of the Data Packet fields is transmitted first.
