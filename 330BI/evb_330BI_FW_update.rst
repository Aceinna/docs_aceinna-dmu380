OpenIMU330BI Firmware Update
==============================

There are two methods that can be used to update the FW in the OpenIMU330BI. 
   - Using the JTAG SWD interface
   - or using the built-in MCU Bootloader, the Boot0 Pin and the UART port. 
Care should be taken during schematic and layout generation to make provisions for either or both of these methods if FW upgrading capability will be needed in the end product.

Using JTAG (SWD) interface 
-------------------------------

OpenIMU330BI has standard SWD interface. Next pins are used: 

+-----------------------+-----------------------+-----------------------+
|        Pin #          |     Pin Function      |         Note          |
+-----------------------+-----------------------+-----------------------+
|        K3             |        SWCLK          |			|
+-----------------------+-----------------------+-----------------------+
|        J2             |        SWDIO          |			|
+-----------------------+-----------------------+-----------------------+
|        F3             |        RESET          |			|
+-----------------------+-----------------------+-----------------------+
|                       |        VIN            | Reference voltage     |
+-----------------------+-----------------------+-----------------------+
|                       |        GND            |		Ground  |
+-----------------------+-----------------------+-----------------------+

SWD interface allows to perform programming of application into unit from development environment or using special utilities, for example ST-Link Utility. 

.. note::

   - Application image should be programmed from address 0x08000000
   - Last 6 sectors of MCU flash should not be erased during programming. They contain calibration parameters.
   - For unit to work properly last 6 sectors need to be write-protected. Write protection performed at the factory but in case of unit recovery it needs to be performed again.
   - To be able to recover unit read and save full original image first (from address 0x08000000, length 0x20000).  


Using built-in MCU bootloader
---------------------------------

Application image can be programmed into the unit via serial interface using built into the processor boot loading capability.

Next pins on OpenIMU330BI are used in this case:

+-----------------------+--------------------------+-----------------------+
|        Pin #          |     Pin Function         |         Notes         |
+-----------------------+--------------------------+-----------------------+
|        K1             |        BOOT0             |		 3.3 V     |
+-----------------------+--------------------------+-----------------------+
|        G7             | USER_UART_RX (to unit)   |		0 – 3.3V   |
+-----------------------+--------------------------+-----------------------+
|        F1             | USER_USRT_TX (from unit) |		0 – 3.3V   |
+-----------------------+--------------------------+-----------------------+
|        F3             |        RESET             |	0 – 3.3V Optional  |
+-----------------------+--------------------------+-----------------------+
|                       |        GND               |		           |
+-----------------------+--------------------------+-----------------------+

Next sequence needs to be executed to force unit into boot loading mode:

1.	Connect serial RS232 interface from PC to unit using RS232-TTL convertor. There may be also direct USB-TTL serial adapter.
2.	Provide HIGH level on BOOT0 pin.
3.	Power up unit or apply RESET signal (active low. Time > 10 milliseconds).
4.	Start custom boot loading utility or ST Micro utility and follow the steps in the documentation. 

User can choose to implement their own boot loader or use utilities provided by ST-Micro.

In first case find boot loading application note AN3155 here:

 `<https://www.st.com/content/st_com/en/search.html#q=AN3155-t=resources-page=1>`__

In second case find ST Flash Loader Utility here:

 `<https://www.st.com/en/development-tools/flasher-stm32.html>`__


.. note::

   - In case if unit is not recognized by ST Flash Loader, place file STM32L4_128K.STmap (download below) into MAP directory (created during tool installation)

   - Application image should be programmed from address 0x08000000
   - Last 6 sectors of MCU flash should not be erased during programming. They contain calibration parameters.
   - For unit to work properly last 6 sectors need to be write-protected. Write protection performed at the factory but in case of unit recovery it needs to be performed again.
   - To be able to recover unit read and save full original image first (from address 0x08000000, length 0x20000).  


File STM32L4_128K.STmap :download:`download <./_docs/STM32L4_128K.STmap>`
