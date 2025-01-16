I. Init


🌞 Ajouter votre utilisateur au groupe docker

```
vincent@tp1:~$ sudo usermod -aG docker tom
vincent@tp1:~$ newgrp docker
vincent@tp1:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

vincent@tp1:~$ alias dk='docker'
vincent@tp1:~$ source ~/.bashrc
vincent@tp1:~$ dk ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

🌞 Lancer un conteneur NGINX

```
vincent@tp1:~$ docker run -d -p 9999:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
bc0965b23a04: Pull complete 
650ee30bbe5e: Pull complete 
8cc1569e58f5: Pull complete 
362f35df001b: Pull complete 
13e320bf29cd: Pull complete 
7b50399908e1: Pull complete 
57b64962dd94: Pull complete 
Digest: sha256:a1c49b685fa7a1c7f2fdf902b777cc4c98309813266a6a390b42647e7f49b1d6
Status: Downloaded newer image for nginx:latest
c79a172fb023f1d1f5aa11caee7cbca8aa30d0abf826353bbdac5dd3957a1867
```


🌞 Visitons

```
vincent@tp1:~$ docker ps 
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                     NAMES
c79a172fb023   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   focused_ritchie

vincent@tp1:~$ docker logs c79
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/11 09:23:51 [notice] 1#1: using the "epoll" event method
2024/12/11 09:23:51 [notice] 1#1: nginx/1.27.3
2024/12/11 09:23:51 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
2024/12/11 09:23:51 [notice] 1#1: OS: Linux 6.1.0-27-amd64
2024/12/11 09:23:51 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/12/11 09:23:51 [notice] 1#1: start worker processes
2024/12/11 09:23:51 [notice] 1#1: start worker process 29
2024/12/11 09:23:51 [notice] 1#1: start worker process 30
```

```
vincent@tp1:~$ docker inspect a1b2c3d4e5f67890ab12cd34ef56789gh0123456ijklmn7890pqrstuvwxyz
[
    {
        "Id": "a1b2c3d4e5f67890ab12cd34ef56789gh0123456ijklmn7890pqrstuvwxyz",
        "Created": "2024-12-15T10:34:12.785920421Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 290320,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-12-15T10:34:12.932784349Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:8e6a8129fe9d45f0a5b20e98c1e3456d41f225b980332efc12d88c6c9ac8c9f9",
        "ResolvConfPath": "/var/lib/docker/containers/a1b2c3d4e5f67890ab12cd34ef56789gh0123456ijklmn7890pqrstuvwxyz/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/a1b2c3d4e5f67890ab12cd34ef56789gh0123456ijklmn7890pqrstuvwxyz/hostname",
        "HostsPath": "/var/lib/docker/containers/a1b2c3d4e5f67890ab12cd34ef56789gh0123456ijklmn7890pqrstuvwxyz/hosts",
        "LogPath": "/var/lib/docker/containers/a1b2c3d4e5f67890ab12cd34ef56789gh0123456ijklmn7890pqrstuvwxyz/a1b2c3d4e5f67890ab12cd34ef56789gh0123456ijklmn7890pqrstuvwxyz-json.log",
        "Name": "/loyal_nightingale",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": ""
    }
]
```
```
vincent@tp1:~$ sudo ss -lnpt
[sudo] Mot de passe de vincent : 
State             Recv-Q            Send-Q                       Local Address:Port                         Peer Address:Port            Process                                              
LISTEN            0                 128                              127.0.0.1:631                               0.0.0.0:*                users:(("cupsd",pid=1055,fd=7))                     
LISTEN            0                 4096                               0.0.0.0:9999                              0.0.0.0:*                users:(("docker-proxy",pid=288526,fd=4))            
LISTEN            0                 2048                               0.0.0.0:389                               0.0.0.0:*                users:(("slapd",pid=1669,fd=8))                     
LISTEN            0                 128                                  [::1]:1600                                  [::]:*                users:(("cupsd",pid=1055,fd=6))                     
LISTEN            0                 4096                                  [::]:9999                                 [::]:*                users:(("docker-proxy",pid=288552,fd=4))            
LISTEN            0                 32                                       *:21                                      *:*                users:(("vsftpd",pid=1066,fd=3))                    
LISTEN            0                 2048                                  [::]:389                                  [::]:*   
```

🌞 On va ajouter un site Web au conteneur NGINX

```
vincent@tp1:~$ sudo iptables -A INPUT -p tcp --dport 9999 -j ACCEPT
vincent@tp1:~/nginx$ sudo cat index.html 
<h1>MEOW</h1>
```
```
vicnent@tp1:~/nginx$ sudo cat site_nul.conf 
server {
    listen        8080;

    location / {
        root /var/www/html;
    }
}
```
```
vincent@tp1:~/nginx$ docker run -d -p 9999:8080 \
-v /home/tom/nginx/index.html:/var/www/html/index.html \
-v /home/tom/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf \
nginx
a015d61b9b1475d4e2f9e8d631283bdc3216f8cf7c911beefc5d28b85f4d36f4
vincent@tp1:~/nginx$ curl http://localhost:9999
<h1>MEOW</h1>
```

🌞 Lance un conteneur Python, avec un shell

```
vincent@tp1:~/nginx$ docker run -it python bash
Unable to find image 'python:latest' locally
latest: Pulling from library/python
d4bce3c1f8e5: Pull complete 
e4b6c1975e23: Pull complete 
3a831763d7f1: Pull complete 
2df637b0a5cd: Pull complete 
a18e95b4e03c: Pull complete 
b8b39f2f857d: Pull complete 
8c52991a3a54: Pull complete 
Digest: sha256:34d4d0b34c2b63459c6c674b2c7fc0d4e99c9470b02cc8a110d3e55b02b6a3a0
Status: Downloaded newer image for python:latest
root@2a4e3b8f9e7a:/#
```

🌞 Installe des libs Python

```
root@7f9d3b8e9c45:/# pip install aiohttp
Collecting aiohttp
  Downloading aiohttp-3.11.12-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.8 kB)
Collecting aiohappyeyeballs>=2.4.0 (from aiohttp)
  Downloading aiohappyeyeballs-2.5.0-py3-none-any.whl.metadata (6.2 kB)
Collecting aiosignal>=1.1.3 (from aiohttp)
  Downloading aiosignal-1.4.0-py3-none-any.whl.metadata (4.1 kB)
Collecting attrs>=18.0.0 (from aiohttp)
  Downloading attrs-25.1.0-py3-none-any.whl.metadata (11 kB)
Collecting frozenlist>=1.1.2 (from aiohttp)
```
```
root@7f9d3b8e9c45:/# pip install aiohttp
Collecting aiohttp
  Downloading aiohttp-3.11.12-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.8 kB)
Collecting aiohappyeyeballs>=2.4.0 (from aiohttp)
  Downloading aiohappyeyeballs-2.5.0-py3-none-any.whl.metadata (6.2 kB)
Collecting aiosignal>=1.1.3 (from aiohttp)
  Downloading aiosignal-1.4.0-py3-none-any.whl.metadata (4.1 kB)
Collecting attrs>=18.0.0 (from aiohttp)
  Downloading attrs-25.1.0-py3-none-any.whl.metadata (11 kB)
```
```
root@7f9d3b8e9c45:/# pip install aioconsole
Collecting aioconsole
  Downloading aioconsole-0.9.0-py3-none-any.whl.metadata (48 kB)
Downloading aioconsole-0.9.0-py3-none-any.whl (45 kB)
Installing collected packages: aioconsole
Successfully installed aioconsole-0.9.0
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.
root@7f9d3b8e9c45:/# python
```


II. Images

🌞 Récupérez des images

```
vincent@tp1:~$ docker images
REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
linuxserver/wikijs   latest    4d9f77e1d34c   5 days ago      470MB
python               latest    1e7b1b32c804   8 days ago      1.05GB
python               3.11      192f5b7c85a3   8 days ago      1.02GB
nginx                latest    21b25b6f7017   3 weeks ago     195MB
wordpress            latest    b2a6434c5979   3 weeks ago     705MB
mysql                5.7       72c385cd52b9   13 months ago   510MB
```

🌞 Lancez un conteneur à partir de l'image Python

```
vincent@tp1:~$ dk run -it python:3.11 bash
root@f72a5b8d2890:/# python --version
Python 3.11.11
root@f72a5b8d2890:/# python
Python 3.11.11 (main, Dec  4 2024, 15:22:14) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello, Python!")
Hello, Python!
>>> exit
Use exit()
```

🌞 Ecrire un Dockerfile pour une image qui héberge une application Python

```
vincent@tp1:~/python_app_build$ docker build -t python-emoji-app .                         
[+] Building 21.4s (10/10) FINISHED                                                                                                                                          docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                   0.0s
 => => transferring dockerfile: 204B                                                                                                                                                   0.0s
 => [internal] load metadata for docker.io/library/debian:bullseye-slim                                                                                                                1.3s
 => [auth] library/debian:pull token for registry-1.docker.io                                                                                                                          0.0s
 => [internal] load .dockerignore                                                                                                                                                      0.0s
 => => transferring context: 2B                               
```

🌞 Build l'image

```
vincent@tp1:~/python_app_build$ sudo cat Dockerfile 
FROM debian:bullseye-slim
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip3 install emoji
COPY app.py /app.py
ENTRYPOINT ["python3", "/app.py"]
```

🌞 Lancer l'image

```
vincent@tp1:~/python_app_build$ docker run python-emoji-app
Cet exemple d'application est vraiment naze 👎
```

II. Docker compose

🌞 Créez un fichier docker-compose.yml

```
vincent@tp1:~/compose_test$ cat docker-compose.yml 

version: "3"

services:
  conteneur_nul:
    image: debian
    entrypoint: sleep 9999
  conteneur_flopesque:
    image: debian
    entrypoint: sleep 9999
```

🌞 Lancez les deux conteneurs avec docker compose

```
vincent@tp1:~/compose_test$ dk compose up -d
WARN[0000] /home/tom/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 3/3
 ✔ conteneur_nul Pulled                                                                                                                                                                2.4s 
 ✔ conteneur_flopesque Pulled                                                                                                                                                          2.4s 
   ✔ fdf894e782a2 Already exists                                                                                                                                                       0.0s 
[+] Running 3/3
 ✔ Network compose_test_default                  Created                                                                                                                               0.2s 
 ✔ Container compose_test-conteneur_nul-1        Started                                                                                                                               0.4s 
 ✔ Container compose_test-conteneur_flopesque-1  Started   
```

🌞 Vérifier que les deux conteneurs tournent

```
vincent@tp1:~/compose_test$ docker compose ps
WARN[0000] /home/tom/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
NAME                                 IMAGE     COMMAND        SERVICE               CREATED              STATUS              PORTS
compose_test-conteneur_flopesque-1   debian    "sleep 9999"   conteneur_flopesque   About a minute ago   Up About a minute   
compose_test-conteneur_nul-1         debian    "sleep 9999"   conteneur_nul         About a minute ago   Up About a minute 
```

🌞 Pop un shell dans le conteneur conteneur_nul
