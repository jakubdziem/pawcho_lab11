### Tworzenie sieci Docker

```
docker network create --driver=bridge --subnet=192.168.0.0/16 lab11net
```

---

### Uruchomienie kontenera `web1`

```
docker run -d ^
  --name web1 ^
  --network lab11net --ip=192.168.0.2 ^
  -p 8081:80 ^
  --mount type=bind,source="C:\Users\jakub\lab11\pawcho_lab11\index",target=/usr/share/nginx/html,readonly ^
  --mount type=bind,source="C:\Users\jakub\lab11\lab11\web1",target=/var/log/nginx ^
  nginx:latest
```

![web1](https://github.com/user-attachments/assets/838fd065-bdf2-4d77-bfb6-aa976efdcee7)

---

### Uruchomienie kontenera `web2`

```
docker run -d ^
  --name web2 ^
  --network lab11net --ip=192.168.0.3 ^
  -p 8082:80 ^
  --mount type=bind,source="C:\Users\jakub\lab11\pawcho_lab11\index",target=/usr/share/nginx/html,readonly ^
  --mount type=bind,source="C:\Users\jakub\lab11\lab11\web2",target=/var/log/nginx ^
  nginx:latest
```

![web2](https://github.com/user-attachments/assets/860c4b23-8a3f-48e5-b854-0ad0e30bf9e7)

---

### Uruchomienie kontenera `web3`

```
docker run -d ^
  --name web3 ^
  --network lab11net --ip=192.168.0.4 ^
  -p 8083:80 ^
  --mount type=bind,source="C:\Users\jakub\lab11\pawcho_lab11\index",target=/usr/share/nginx/html,readonly ^
  --mount type=bind,source="C:\Users\jakub\lab11\lab11\web3",target=/var/log/nginx ^
  nginx:latest
```

![web3](https://github.com/user-attachments/assets/4812340e-3c58-4625-8c3a-56503d85ef65)

---

### Struktura katalogów z logami

```
C:\Users\jakub\lab11\lab11>tree /f /a

Folder PATH listing for volume Windows
Volume serial number is 1C55-7C0C
C:.
+---web1
|       access.log
|       error.log
|
+---web2
|       access.log
|       error.log
|
\---web3
        access.log
        error.log
```

---

### Zawartość katalogu z plikiem `index.html`

```
C:\Users\jakub\lab11\pawcho_lab11\index>dir

20.05.2025  18:28    <DIR>          .
20.05.2025  18:28    <DIR>          ..
20.05.2025  16:35               208 index.html
               1 File(s)            208 bytes
```

---

### Lista działających kontenerów

```
docker ps

CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS         PORTS                  NAMES
4d4db289152f   nginx:latest  "/docker-entrypoint.…"   7 minutes ago   Up 7 minutes   0.0.0.0:8083->80/tcp   web3
c998c417c646   nginx:latest  "/docker-entrypoint.…"   7 minutes ago   Up 7 minutes   0.0.0.0:8082->80/tcp   web2
800f50e27beb   nginx:latest  "/docker-entrypoint.…"   9 minutes ago   Up 9 minutes   0.0.0.0:8081->80/tcp   web1
```
