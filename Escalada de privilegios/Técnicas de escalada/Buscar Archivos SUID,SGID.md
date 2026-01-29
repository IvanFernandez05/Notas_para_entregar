```bash
# Archivos SUID (ejecutan con permisos del propietario)
find / -type f -perm -4000 2>/dev/null

# Archivos SGID (ejecutan con permisos del grupo)
find / -type f -perm -2000 2>/dev/null

# Ambos
find / -type f \( -perm -4000 -o -perm -2000 \) 2>/dev/null

# Búsqueda más detallada con información
find / -type f -perm -4000 -exec ls -la {} \; 2>/dev/null
```

Binarios mas explotables:
- No comunes, que no hayamos visto en otras máquinas
- systemctl
- find
- cp
- mv
- python
- tar
- apt
- vim
- nmap
- bash
