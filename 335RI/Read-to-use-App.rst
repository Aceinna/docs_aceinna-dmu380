Vertical Gyro (VG) Application 
=================================================

.. contents:: Contents
    :local:




The Vertical Gyro (VG) application 
supports all of the features and operating modes of the
IMU APP, and it links in additional internal software, running on the
processor, for the computation of dynamic roll, pitch. 
Roll, Pitch measurements are often referred to as "VG" or Vertical Gyro measurements.


At a fixed 200Hz rate, the VG APP continuously maintains the digital
IMU data as well as the dynamic roll, pitch. After the Sensor Calibration Block, 
the IMU data is 
passed to the Integration to Orientation block. The Integration to
Orientation block integrates body frame sensed angular rate to
orientation at a fixed 200 times per second within all of the OpenIMU
Series products.

The Integration to 
Orientation block receives drift corrections from the Extended Kalman
Filter or Drift Correction Module. In general, rate sensors and
accelerometers suffer from bias drift, misalignment errors, acceleration
errors (g-sensitivity), nonlinearity (square terms), and scale factor
errors. The largest error in the orientation propagation is associated
with the rate sensor bias terms. The Extended Kalman Filter (EKF) module
provides an on-the-fly calibration for drift errors, including the rate
sensor bias, by providing corrections to the Integration to Orientation
block and a characterization of the gyro bias state. In the VG APP,
the internally computed gravity reference vector provide an attitude
reference measurement for the EKF when the unit is in quasi-static
motion to correct roll, pitch angle drift and to estimate
the X, Y and Z gyro rate bias. The VG APP adaptively tunes the EKF
feedback gains in order to best balance the bias estimation and 
correction with distortion free performance during dynamics when the
object is accelerating either linearly (speed changes) or centripetally
(false gravity forces from turns). Because centripetal and other dynamic
accelerations are often associated with yaw rate, the VG APP
maintains a low-passed filtered yaw rate signal and compares it to the
turnSwitch threshold field (user adjustable). When the user platform
exceeds the turnSwitch threshold yaw rate,
the VG APP lowers the feedback gains from the accelerometers to allow
the attitude estimate to coast through the dynamic situation with
primary reliance on angular rate sensors. This situation is indicated by
the softwareStatus - turnSwitch status flag. Using the turn switch
maintains better attitude accuracy during short-term dynamic situations,
but care must be taken to ensure that the duty cycle of the turn switch
generally stays below 10% during the vehicle mission. A high turn switch
duty cycle does not allow the system to apply enough rate sensor bias
correction and could allow the attitude estimate to become unstable.

The VG APP algorithm also has two major phases of operation. The first phase of
operation is the attitude initialization phase. During the
initialization phase, the OpenIMU unit is expected to be stationary or
quasi-static to rapidly estimate the X, Y, and Z rate sensor bias, and the initial attitude.
The initialization phase lasts approximately 2 seconds.
After the initialization phase, the EKF algorithm in the VG APP dynamically tunes the
feedback (also referred to as EKF gain) from the accelerometers continuously estimate and correct for roll, pitch errors, as well as to estimate X, Y, and Z rate sensor
bias.

VG App Output Packets Definitions
----------------------------------------------------------------

"a1" packet
^^^^^^^^^^^^

The default VG app output packet type is "a1", and it is defined in the following two tables.

    +----------------------+-------------+--------+----------------+-------------+
    ||  ('a1' = 0x6131)    |             |        |                |             |
    +----------------------+-------------+--------+----------------+-------------+
    || Preamble            || Packet Type|| Length|| Payload       || Termination|
    +----------------------+-------------+--------+----------------+-------------+
    || 0x5555              || 0x6131     ||  47   ||               || <CRC (U2)> |
    +----------------------+-------------+--------+----------------+-------------+

    Payload:

    +-----------+--------------------------+-----------+-----------+
    || Byte     || Name                    || Format   || Notes    |
    || Offset   ||                         ||          ||          |
    +-----------+--------------------------+-----------+-----------+
    || 0        || System Timer of         || U4       || LSB First|
    ||          || sensors sampling        ||          || msec     |
    +-----------+--------------------------+-----------+-----------+
    || 4        || Above timer converted   || D        || LSB First|
    ||          || to a double type        ||          || second   |
    +-----------+--------------------------+-----------+-----------+
    || 12       || Roll                    || F4       || LSB First|
    ||          ||                         ||          || deg      |
    +-----------+--------------------------+-----------+-----------+
    || 16       || Pitch                   || F4       || LSB First|
    ||          ||                         ||          || deg      |
    +-----------+--------------------------+-----------+-----------+
    || 20       || corrected X gyro        || F4       || LSB First|
    ||          ||                         ||          || deg/s    |
    +-----------+--------------------------+-----------+-----------+
    || 24       || corrected Y gyro        || F4       || LSB First|
    ||          ||                         ||          || deg/s    |
    +-----------+--------------------------+-----------+-----------+
    || 28       || corrected Z gyro        || F4       || LSB First|
    ||          ||                         ||          || deg/s    |
    +-----------+--------------------------+-----------+-----------+
    || 32       || X Accel                 || F4       || LSB First|
    ||          ||                         ||          || m/s/s    |
    +-----------+--------------------------+-----------+-----------+
    || 36       || Y Accel                 || F4       || LSB First|
    ||          ||                         ||          || m/s/s    |
    +-----------+--------------------------+-----------+-----------+
    || 40       || Z Accel                 || F4       || LSB First|
    ||          ||                         ||          || m/s/s    |
    +-----------+--------------------------+-----------+-----------+
    || 44       || Operation mode [1]_     || U1       || LSB First|
    ||          ||                         |           ||          |
    +-----------+--------------------------+-----------+-----------+
    ||  45      || Linear accel switch [2]_|| U1       || LSB First|
    ||          ||                         ||          ||          |
    +-----------+--------------------------+-----------+-----------+
    || 46       || Turn switch [3]_        || U1       || LSB First|
    ||          ||                         ||          ||          |
    +-----------+--------------------------+-----------+-----------+

"a2" packet
^^^^^^^^^^^^

If you want to output the yaw angle, you can choose the "a2" packet. For the VG app, the yaw angle is from integrating the gyro rate.


    +----------------------+-------------+--------+----------------+-------------+
    ||  ('a2' = 0x6132)    |             |        |                |             |
    +----------------------+-------------+--------+----------------+-------------+
    || Preamble            || Packet Type|| Length|| Payload       || Termination|
    +----------------------+-------------+--------+----------------+-------------+
    || 0x5555              || 0x6132     ||  48   ||               || <CRC (U2)> |
    +----------------------+-------------+--------+----------------+-------------+

    Payload:

    +-----------+--------------------------+-----------+-----------+
    || Byte     || Name                    || Format   || Notes    |
    || Offset   ||                         ||          ||          |
    +-----------+--------------------------+-----------+-----------+
    || 0        || System Timer of         || U4       || LSB First|
    ||          || sensors sampling        ||          || msec     |
    +-----------+--------------------------+-----------+-----------+
    ||  4       || Above timer converted   || D        || LSB First|
    ||          || to a double type        |           || second   |
    +-----------+--------------------------+-----------+-----------+
    ||  12      || Roll                    || F4       || LSB First|
    ||          ||                         ||          || deg      |
    +-----------+--------------------------+-----------+-----------+
    ||  16      || Pitch                   || F4       || LSB First|
    ||          ||                         ||          || deg      |
    +-----------+--------------------------+-----------+-----------+
    ||  20      || Yaw                     || F4       || LSB First|
    ||          ||                         ||          || deg      |
    +-----------+--------------------------+-----------+-----------+
    ||  24      || corrected X gyro        || F4       || LSB First|
    ||          ||                         ||          || deg/s    |
    +-----------+--------------------------+-----------+-----------+
    ||  28      || corrected Y gyro        || F4       || LSB First|
    ||          ||                         ||          || deg/s    |
    +-----------+--------------------------+-----------+-----------+
    || 32       || corrected Z gyro        || F4       || LSB First|
    ||          ||                         ||          || deg/s    |
    +-----------+--------------------------+-----------+-----------+
    ||  36      || X Accel                 || F4       || LSB First|
    ||          ||                         ||          || m/s/s    |
    +-----------+--------------------------+-----------+-----------+
    ||  40      || Y Accel                 || F4       || LSB First|
    ||          ||                         ||          || m/s/s    |
    +-----------+--------------------------+-----------+-----------+
    ||  44      || Z Accel                 || F4       || LSB First|
    ||          ||                         ||          || m/s/s    |
    +-----------+--------------------------+-----------+-----------+


    
.. [1] Operation mode of the algorithm. 0 for waiting for the system to stabilize, 1 for initialzing attiude,
        2 and 3 for VG mode, and 4 for INS mode. Please refer to the source code for details.
.. [2] 0 if linear acceleration is detected, 1 if no linear acceleration. Please refer to the source code for details.
.. [3] Indicate if the filtered yaw rate exceeds the turn switch threshold. 1 yes, 0 no. Please refer to the source code for details.






.. contents:: Contents
    :local:



