```bash
# Información del kernel
cat /proc/version
uname -a
uname -r

# Buscar exploits
# En tu máquina con searchsploit
searchsploit linux kernel <version>
searchsploit linux kernel 4.4.0

# Recursos online
# https://www.exploit-db.com/
# https://github.com/lucyoa/kernel-exploits
```

Exploits de kernel famosos:

|Nombre|Versiones afectadas|CVE|
|---|---|---|
|Dirty COW|2.6.22 - 4.8.3|CVE-2016-5195|
|Dirty Pipe|5.8+|CVE-2022-0847|
|PwnKit|Polkit (2009-2022)|CVE-2021-4034|

