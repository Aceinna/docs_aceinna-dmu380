WARNING!!!! Before You Start Development
========================================


**Before You start developing it is recommended to read whole unit image and save it to binary file to be able to recover unit if something unexpected happened**

Unit image consists of:

1. Bootloader
2. Original (factory) application image
3. Calibration and Configuration partitions. 

**If bootloader or calibration tables are damaged - unit will not work properly!!!.**

Save unit image:
-------------------

1. Install ST-Link Utility from here: https://www.st.com/en/development-tools/stsw-link004.html
2. Connect ST-Link debugger to OpenIMU Evaluation Kit. and to PC
3. Power On Evaluation Kit
4. Start ST-Link utility on your PC.
5. Click Device->Connect.
6. Enter value **0x80000 for OpenIMU300** and **0x20000 for OpenIMU330** into Size box and hit enter
7. Click File->SaveAs and save image to well known location. For OpenIMU300 image size should be 512K bytes. For OpenIMU330 image size should be 128 KBytes.
   
    .. image:: media/UnitImageSave.png

Recover unit image:
----------------------

1. Connect ST-Link debugger to OpenIMU Evaluation Kit. and to PC
2. Power On Evaluation Kit
3. Start ST-Link utility on your PC.
4. Click Device->Connect.
5. Click File->open and open previously saved file.
6. Click Target->Program&Verify.
7. Make sure that **Start address is 0x08000000** and click Start.

    .. image:: media/UnitImageRestore.png


8. After reprogramming of **OpenIMU300** unit (RI or ZI) perform write protection of sectors 0 and 2
9. After reprogramming of **OpenIMU330BI** unit perform write protection of last 6 sectors (58 to 63)

    .. image:: media/UnitImageProtect.png
