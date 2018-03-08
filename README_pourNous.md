# IMA/EVM

Readme juste histoire qu'on se rappelle ce qu'on a fait.

## Sommaire

1) IMA
2) IMA Appraisal
3) EVM

## IMA

### Check if IMA is enable and add&enable it if not

If the path /sys/kernel/security/ima exists > IMA is already installed
Else : Rebuilt the kernel with an additionnal .config file and write in it :
```
CONFIG_INTEGRITY=y
CONFIG_IMA=y
CONFIG_IMA_MEASURE_PCR_IDX=10
CONFIG_IMA_AUDIT=y
CONFIG_IMA_LSM_RULES=y
```

Then, to enable just go into the /etc/default/grub configuration file and edit the line GRUB_CMDLINE_LINUX="" like this :
```
GRUB_CMDLINE_LINUX="ima_tcb"
```

Then update the file /boot/grub/grub.cfg with the command :
```
sudo update-grub
```

(Ici j'ai redémarrer mon ubuntu, je sais pas si c'est utile, à tester)

### Try a violation

The default IMA policy check all the files that root can read, so you can choose any files permissions with the command
```
ls -la
```

Find a file that root can edit (ici j'ai pris /etc/mysql/mysql.cnf) and change what you want.
Then restart your machine and go to /sys/kernel/security/ima and check the file violations, it should be increased by 1.

... not finished yet ............................................................................................................................

## IMA Appraisal

### Enable IMA appraisal

When rebuilt the kernel, add in the same .config file of IMA :
```
CONFIG_INTEGRITY_SIGNATURE=y
CONFIG_INTEGRITY=y
CONFIG_IMA_APPRAISE=y
```

... not finished yet ............................................................................................................................

## EVM

### Enable EVM

EVM has a dependency on encrypted keys, which should be encrypted/decrypted using a trusted key. 
For those systems without a TPM, the EVM key could be encrypted/decrypted with a user-defined key instead. 
For EVM, enable the following .config options:
```
CONFIG_TCG_TPM=y

CONFIG_KEYS=y
CONFIG_TRUSTED_KEYS=y
CONFIG_ENCRYPTED_KEYS=y

CONFIG_INTEGRITY_SIGNATURE=y
CONFIG_INTEGRITY=y
CONFIG_EVM=y
```

... not finished yet ............................................................................................................................