```bash
# Ver contenido actual
cat /etc/sudoers
ls -la /etc/sudoers.d/

# Si tienes permisos de escritura
# Añadir usuario con privilegios totales
echo "usuario ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Alternativa: usar visudo si está disponible
# Esto valida la sintaxis antes de guardar
export EDITOR=nano
sudo visudo
```

**TENER CUIDADO**: Un error de sintaxis en sudoers puede bloquear el acceso sudo para todos.

