# Ima Install

Describing how to enable IMA on AGL (with intel-core-i7 board)

## Manually

After setting launching the aglsetup.sh, launch the config menu.
`bitbake -c menuconfig`
In security, activate IMA //TODO Exact option
Then add some more options (setting the ima_policy file ...)
Add the boot parameters "ima_tcb" and 'ima_appraise_tcb'

## Yocto Recipe
//TODO make this recipe work
Add the meta-integrity feature to the aglsetup.sh. This recipe is for devel only, as it use the default keys.
This recipe is based on the meta-intel-iot-security/meta-integrity, and add some options like :
- in the conf file :
`
INHERIT += "ima-evm-rootfs"
IMA_EVM_KEY_DIR = "${IMA_EVM_BASE}/data/debug-keys"
IMA_EVM_ROOTFS_FILES = "usr sbin bin lib -type f"
`
