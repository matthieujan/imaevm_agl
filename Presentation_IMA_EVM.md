# Introduction to IMA/EVM

## IMA

IMA is a three components feature activable in the linux Kernel.
The three component are : 
- IMA-measurement which maintains a runtime measurement list and a integrity value over this list.
To avoid the compromision of this list, it can be anchored in a spécific hardware (TPM).
- IMA-appraisal which verifying file's integrity before transferring control or allowing te file to be accessed by the OS at the boot of the system.
- IMA-audit which includes files hashes in the system's logs.


To sum up, IMA measuring the integrity of files that are loaded before it's executed or record in the memory. It also provide logs that can be consulted. It calculate hash values for files and log them based on configurable policy.

## IMA's problems

IMA present some problems that express why we don't recommend its use as part of the AGL project.

First of all, IMA doesnt protect directories. That allows attackers to remove configuration file and replace it with link to unprotected directory.

If a hostile application has managed to take over the system, he will be able to corrupt the list from the IMA modules: this makes IMA useless. That why IMA must be use in association with a TPM chip. A Trusted Platform Module is a hardware secure cryptoprocessor wich is use for secure boot and key storage.

IMA modules are initialized during the boot. If and attacker gain control of the kernel before the initialisation, IMA is useless.

At this time, the default cryptographic hash function is SHA1, which is not really secure now. Apparently, the system can be configured with SHA256 but is not yet implemented.

IMA have some problems in production, especially in IOT : if a power loss happen, the files can be unreadable; that can be a huge problem for configuration or security files. IMA rehash the file when the process is well closed (like a function "close()" is called).

## Conclusion on IMA

To conclude, IMA is a great tool to check the integrity of the files of our system, but concretely, it is not yet mature enough to be exploited in production on a project such as AGL.

## Source of informations

https://code.woboq.org/linux/linux/security/integrity/ima/ima_main.c.html
https://lwn.net/Articles/137306/
https://lwn.net/Articles/733431/
https://lwn.net/Articles/137311/
