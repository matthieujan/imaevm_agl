# Introduction to IMA/EVM

## IMA

IMA is a three components feature activable in the linux Kernel.
The three component are : 
- IMA-measurement which maintains a runtime measurement list and a integrity value over this list.
To avoid the compromision of this list, it can be anchored in a spécific hardware (TPM).
- IMA-appraisal which verifying file's integrity before transferring control or allowing te file to be accessed by the OS at the boot of the system.
- IMA-audit which includes files hashes in the system's logs.


To sum up, IMA measuring the integrity of files that are loaded before it's executed or record in the memory. It also provide logs that can be consulted.

IMA problems in production :
IMA doesnt protect direcotry, that allows attackers to remove configuration file and replace it whith link to unprotected directory.

In IOT, if a power loss happen, files can be unreadable. IMA rehash the file when the process is well closed.
