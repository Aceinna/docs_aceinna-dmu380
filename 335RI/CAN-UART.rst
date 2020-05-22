CAN and UART
============

.. contents:: Contents
    :local:

Ports
----------------

The OpenIMU335RI has two external ports; one UART port and one CAN bus port.
Based on these available external ports, the OpenIMU335RI can be configured
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


UART Messaging
----------------

To learn more about the OpenIMU UART Messaging Framework, please see the following pages: 


1. `UART Messsaging Framework <../software/UARTmessaging.html#OpenIMU UART Messaging Framework>`__


CAN Messaging
----------------


**CAN J1939 Example Application For OpenIMU335RI**

	
*   The SAE J1939 standards document set specifies the requirements for systems based on J1939 messaging.
    The SAE site provides a full list of the J1939 standard document set - `Link <https://www.sae.org/standardsdev/groundvehicle/j1939a.htm>`_
*   In particular:

    *   Section 3 of the SAE J1939 standards document provides the high-level technical requirements
        for systems that use J1939 messaging.
    *   Section 5 of the SAE J1939-21 standards document provides the technical requirements
        for J1939 data link layer for all SAE J1939 applications.
    *   The license for using an SAE standards document do not allow distribution of the documents.
        SAE J1939 documents can be purchased online at the IHS Standards Store -
        `Link <https://global.ihs.com/search_res.cfm?&rid=Z56&mid=SAE&input_doc_number=J1939&input_doc_title=&sort=RELEVANCE>`_
    *   There are many J1939 related documents available that can be freely distributed.  We provide two such documents here:

        *   Vector Informatik GmbH provides a document which is a good introduction to
            J1939 :download:`download link <../media/Vector AN-ION-1-3100_Introduction_to_J1939.pdf>`.
        *   Kvaser provides a J1939 Overview document - :download:`download link <../media/Kvaser-J1939-Overview.pdf>`.

.. note::   **If you use any links here, user your browser back button to return**

The following pages describe the CAN Messaging Details:

*   SAE J1939 & Custom CAN messages implemented for OpenIMU335RI.


