TP2 : Utilisation courante de Docker

I. Commun à tous : App Web
II Dév. Python
II Admin. Maîtrise de la stack Web
II Secu. Big brain


I. Commun à tous : App Web

Voir docker_tp2


II Dév. Python


1. Calculatrice

https://github.com/vincent4player/calculatrice.git

2. Chat room

https://github.com/vincent4player/chat_room.git

Ur own

https://github.com/vincent4player/Ur-Own.git



II Admin. Maîtrise de la stack Web



I. Good practices

🌞 Limiter l'accès aux ressources

```
vincent@tp2:~$ docker run -dit --memory="1000m" nginx
d1f342ea4098e5447b9bcba05d2fb5e3f8f1c56a9f3b0b47f7d415a4fe63b4d1

vincent@tp2:~$ docker run -dit --cpus="1.0" nginx
47c59385f80d0e1cb5f2bda914984d836b4d557da2a1e768e129fc38fb0f7f5a
```

🌞 No root

```
FROM nginx:latest
RUN useradd -m -s /bin/bash nginxuser
USER nginxuser
```

🌞 Gestion des droits du volume qui contient le code

```
vincent@tp2:~$ sudo chmod -R 755 /app
```

🌞 Gestion des capabilities sur le conteneur NGINX

```
 cap_drop:
      - ALL        
    cap_add:
      - NET_BIND_SERVICE
```

🌞 Mode read-only

```
read_only: true  
```

II. Reverse proxy buddy

🌞 Adaptez le docker-compose.yml de la partie précédente



🌞 HTTPS auto-signé

```
vincent@tp2:~/Repo Git/b2_linux_2024-2025/TP2$ openssl req -new -newkey rsa:4096 -days 365 -nodes -x509 -keyout vincent.supersite.com.key -out vincent.supersite.com.crt
Generating a 4096 bit RSA private key
....................................................................................................................................................................................................................................................................................................................................................++
..............++++
writing new private key to 'vincent.supersite.com.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank.
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:FR
State or Province Name (full name) [Some-State]:France
Locality Name (eg, city) []:Bordeaux
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Vincent
Organizational Unit Name (eg, section) []:vincent
Common Name (e.g. server FQDN or YOUR name) []:vincent
Email Address []:vincent@gmail.com
```

🌞 Générer une clé et un certificat de CA

```
vincent@tp2:~/Repo Git/b2_linux_2024-2025/TP2$ openssl genrsa -des3 -out CA.key 4096
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:
vincent@tp2:~/Repo Git/b2_linux_2024-2025/TP2$ openssl req -x509 -new -nodes -key CA.key -sha256 -days 1024  -out CA.pem
Enter pass phrase for CA.key:
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:FR
State or Province Name (full name) [Some-State]:France
Locality Name (eg, city) []:Bordeaux 
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Vincent
Organizational Unit Name (eg, section) []:vincent
Common Name (e.g. server FQDN or YOUR name) []:vincent
Email Address []:vincent@gmail.com
```

🌞 Générer une clé et une demande de signature de certificat pour notre serveur web

```
vincent@tp2:~/Repo Git/b2_linux_2024-2025/TP2$ openssl req -new -nodes -out www.supersite.com.csr -newkey rsa:4096 -keyout www.supersite.com.key
...+........+...+....+........+.......+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*....+...+......+...+..+.+........+.......+...+.....+....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*..+..........+.....+.+.....+.......+.....+.......+.....+.+.....+.............+......+.....+......+.............+.........+...+........+......................+..+...+....+.....................+.....+....+.........+..+.......+...+.................+......+............+.......+..+.........+.....................+...............+.........+..........+......+...+...+..+.......+.....+.+........+............+.......+.................+....+..+....+.....+......+....+...+......+......+.....+................+........+....+..+...+..................+.......+..+....+...............+.....+...............+....+...+..+............+....+.................+..........+.............................+...+.+......+..................+...+.........+...........+...................+...........+..........+..............+....+............+.....+.......+..+..................+.+..+..........+........+.+...+..+.....................+......................+......+..+....+...+.....+.+.....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:FR
State or Province Name (full name) [Some-State]:France
Locality Name (eg, city) []:France
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Vincent
Organizational Unit Name (eg, section) []:vincent
Common Name (e.g. server FQDN or YOUR name) []:vincent
Email Address []:vincent@gmail.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:root
An optional company name []:
```

🌞 Faire signer notre certificat par la clé de la CA

vincent@tp2:~/Repo Git/b2_linux_2024-2025/TP2$ openssl x509 -req -in www.supersite.com.csr -CA CA.pem -CAkey CA.key -CAcreateserial -out www.supersite.com.crt -days 500 -sha2
Certificate request self-signature ok
subject=C = FR, ST = France, L = France, O = Vincent, OU = vincent, CN = vincent, emailAddress = vincent@gmail.com
Enter pass phrase for CA.key:

🌞 Ajustez la configuration NGINX

voir ngnix.conf

🌞 Prouvez avec un curl que vous accédez au site web


🌞 Ajouter le certificat de la CA dans votre navigateur


