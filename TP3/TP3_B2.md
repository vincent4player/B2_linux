2. Conf SSH

🌞 Chiffrement fort côté serveur

https://blog.stephane-robert.info/docs/securiser/durcissement/ssh/

🌞 Clés de chiffrement fortes pour le client

https://www.hostinger.fr/tutoriels/generer-cle-ssh

```
[vincent@tp3 ~]$ ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/vincent/.ssh/id_ed25519):
Created directory '/home/vincent/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/vincent/.ssh/id_ed25519
Your public key has been saved in /home/vincent/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:hz2ALw9+pzz6A7IW1slc4U7SXtJl1BICWeWyc/tgomU vincent@localhost.localdomain
The key's randomart image is:
+--[ED25519 256]--+
|        .+oo+o   |
|       .o  o+ .  |
|      .o.o.o..   |
|      ..*+oo     |
|     +oBSo* .    |
|    +.*+o. + .   |
|   . +..o E +    |
|    o  oo* o o   |
|   .  .o=o    .  |
+----[SHA256]-----+
[vincent@tp3 ~]$
```

🌞 Connectez-vous en SSH à votre VM avec cette paire de clés

```
[vincent@tp3 ~]$ ssh -i ~/.ssh/id_ed25519 -vvvv vincent@10.7.1.10
OpenSSH_8.7p1, OpenSSL 3.0.1 14 Dec 2021
debug1: Reading configuration data /etc/ssh/ssh_config
debug3: /etc/ssh/ssh_config line 55: Including file /etc/ssh/ssh_config.d/50-redhat.conf depth 0
debug1: Reading configuration data /etc/ssh/ssh_config.d/50-redhat.conf
debug2: checking match for 'final all' host 10.7.1.10 originally 10.7.1.10
debug3: /etc/ssh/ssh_config.d/50-redhat.conf line 3: not matched 'final'
debug2: match not found
debug3: /etc/ssh/ssh_config.d/50-redhat.conf line 5: Including file /etc/crypto-policies/back-ends/openssh.config depth 1 (parse only)
debug1: Reading configuration data /etc/crypto-policies/back-ends/openssh.config
debug3: gss kex names ok: [gss-curve25519-sha256-,gss-nistp256-sha256-,gss-group14-sha256-,gss-group16-sha512-]
debug3: kex names ok: [curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512]
debug1: configuration requests final Match pass
debug2: resolve_canonicalize: hostname 10.7.1.10 is address
debug1: re-parsing configuration
debug1: Reading configuration data /etc/ssh/ssh_config
debug3: /etc/ssh/ssh_config line 55: Including file /etc/ssh/ssh_config.d/50-redhat.conf depth 0
debug1: Reading configuration data /etc/ssh/ssh_config.d/50-redhat.conf
debug2: checking match for 'final all' host 10.7.1.10 originally 10.7.1.10
debug3: /etc/ssh/ssh_config.d/50-redhat.conf line 3: matched 'final'
debug2: match found
debug3: /etc/ssh/ssh_config.d/50-redhat.conf line 5: Including file /etc/crypto-policies/back-ends/openssh.config depth 1
debug1: Reading configuration data /etc/crypto-policies/back-ends/openssh.config
debug3: gss kex names ok: [gss-curve25519-sha256-,gss-nistp256-sha256-,gss-group14-sha256-,gss-group16-sha512-]
debug3: kex names ok: [curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512]
debug3: expanded UserKnownHostsFile '~/.ssh/known_hosts' -> '/home/vincent/.ssh/known_hosts'
debug3: expanded UserKnownHostsFile '~/.ssh/known_hosts2' -> '/home/vincent/.ssh/known_hosts2'
debug3: ssh_connect_direct: entering
debug1: Connecting to 10.7.1.10 [10.7.1.10] port 22.
debug3: set_sock_tos: set socket 3 IP_TOS 0x48
debug1: Connection established.
debug1: identity file /home/vincent/.ssh/id_ed25519 type 3
debug1: identity file /home/vincent/.ssh/id_ed25519-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_8.7
debug1: Remote protocol version 2.0, remote software version OpenSSH_8.7
debug1: compat_banner: match: OpenSSH_8.7 pat OpenSSH* compat 0x04000000
debug2: fd 3 setting O_NONBLOCK
debug1: Authenticating to 10.7.1.10:22 as 'vincent'
debug1: load_hostkeys: fopen /home/vincent/.ssh/known_hosts: No such file or directory
debug1: load_hostkeys: fopen /home/vincent/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug3: order_hostkeyalgs: no algorithms matched; accept original
debug3: send packet: type 20
debug1: SSH2_MSG_KEXINIT sent
debug3: receive packet: type 20
debug1: SSH2_MSG_KEXINIT received
debug2: local client KEXINIT proposal
debug2: KEX algorithms: curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512,ext-info-c
debug2: host key algorithms: ssh-ed25519-cert-v01@openssh.com,ecdsa-sha2-nistp256-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,sk-ssh-ed25519-cert-v01@openssh.com,sk-ecdsa-sha2-nistp256-cert-v01@openssh.com,rsa-sha2-512-cert-v01@openssh.com,rsa-sha2-256-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ssh-ed25519@openssh.com,sk-ecdsa-sha2-nistp256@openssh.com,rsa-sha2-512,rsa-sha2-256,ssh-rsa
debug2: ciphers ctos: aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr,aes128-gcm@openssh.com,aes128-ctr
debug2: ciphers stoc: aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr,aes128-gcm@openssh.com,aes128-ctr
debug2: MACs ctos: hmac-sha2-256-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha2-256,hmac-sha1,umac-128@openssh.com,hmac-sha2-512
debug2: MACs stoc: hmac-sha2-256-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha2-256,hmac-sha1,umac-128@openssh.com,hmac-sha2-512
debug2: compression ctos: none,zlib@openssh.com,zlib
debug2: compression stoc: none,zlib@openssh.com,zlib
debug2: languages ctos:
debug2: languages stoc:
debug2: first_kex_follows 0
debug2: reserved 0
debug2: peer server KEXINIT proposal
debug2: KEX algorithms: curve25519-sha256,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha256,diffie-hellman-group16-sha512,diffie-hellman-group18-sha512
debug2: host key algorithms: rsa-sha2-512,rsa-sha2-256,ecdsa-sha2-nistp256,ssh-ed25519
debug2: ciphers ctos: aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr,aes128-gcm@openssh.com,aes128-ctr
debug2: ciphers stoc: aes256-gcm@openssh.com,chacha20-poly1305@openssh.com,aes256-ctr,aes128-gcm@openssh.com,aes128-ctr
debug2: MACs ctos: hmac-sha2-256-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha2-256,hmac-sha1,umac-128@openssh.com,hmac-sha2-512
debug2: MACs stoc: hmac-sha2-256-etm@openssh.com,hmac-sha1-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512-etm@openssh.com,hmac-sha2-256,hmac-sha1,umac-128@openssh.com,hmac-sha2-512
debug2: compression ctos: none,zlib@openssh.com
debug2: compression stoc: none,zlib@openssh.com
debug2: languages ctos:
debug2: languages stoc:
debug2: first_kex_follows 0
debug2: reserved 0
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ssh-ed25519
debug1: kex: server->client cipher: aes256-gcm@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: aes256-gcm@openssh.com MAC: <implicit> compression: none
debug1: kex: curve25519-sha256 need=32 dh_need=32
debug1: kex: curve25519-sha256 need=32 dh_need=32
debug3: send packet: type 30
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug3: receive packet: type 31
debug1: SSH2_MSG_KEX_ECDH_REPLY received
debug1: Server host key: ssh-ed25519 SHA256:LiWk49XIVPOBhCg7+FRoMGuM+WQZInba139U+eUhqtM
debug1: load_hostkeys: fopen /home/vincent/.ssh/known_hosts: No such file or directory
debug1: load_hostkeys: fopen /home/vincent/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug3: hostkeys_find_by_key_hostfile: trying user hostfile "/home/vincent/.ssh/known_hosts"
debug1: hostkeys_find_by_key_hostfile: hostkeys file /home/vincent/.ssh/known_hosts does not exist
debug3: hostkeys_find_by_key_hostfile: trying user hostfile "/home/vincent/.ssh/known_hosts2"
debug1: hostkeys_find_by_key_hostfile: hostkeys file /home/vincent/.ssh/known_hosts2 does not exist
debug3: hostkeys_find_by_key_hostfile: trying system hostfile "/etc/ssh/ssh_known_hosts"
debug1: hostkeys_find_by_key_hostfile: hostkeys file /etc/ssh/ssh_known_hosts does not exist
debug3: hostkeys_find_by_key_hostfile: trying system hostfile "/etc/ssh/ssh_known_hosts2"
debug1: hostkeys_find_by_key_hostfile: hostkeys file /etc/ssh/ssh_known_hosts2 does not exist
The authenticity of host '10.7.1.10 (10.7.1.10)' can't be established.
ED25519 key fingerprint is SHA256:LiWk49XIVPOBhCg7+FRoMGuM+WQZInba139U+eUhqtM.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.7.1.10' (ED25519) to the list of known hosts.
debug3: send packet: type 21
debug2: set_newkeys: mode 1
debug1: rekey out after 4294967296 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug3: receive packet: type 21
debug1: SSH2_MSG_NEWKEYS received
debug2: set_newkeys: mode 0
debug1: rekey in after 4294967296 blocks
debug1: Will attempt key: /home/vincent/.ssh/id_ed25519 ED25519 SHA256:hz2ALw9+pzz6A7IW1slc4U7SXtJl1BICWeWyc/tgomU explicit
debug2: pubkey_prepare: done
debug3: send packet: type 5
debug3: receive packet: type 7
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<ssh-ed25519,sk-ssh-ed25519@openssh.com,ssh-rsa,rsa-sha2-256,rsa-sha2-512,ssh-dss,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,sk-ecdsa-sha2-nistp256@openssh.com,webauthn-sk-ecdsa-sha2-nistp256@openssh.com>
debug3: receive packet: type 6
debug2: service_accept: ssh-userauth
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug3: send packet: type 50
debug3: receive packet: type 51
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug3: start over, passed a different list publickey,gssapi-keyex,gssapi-with-mic,password
debug3: preferred gssapi-with-mic,publickey,keyboard-interactive,password
debug3: authmethod_lookup gssapi-with-mic
debug3: remaining preferred: publickey,keyboard-interactive,password
debug3: authmethod_is_enabled gssapi-with-mic
debug1: Next authentication method: gssapi-with-mic
debug1: No credentials were supplied, or the credentials were unavailable or inaccessible
No Kerberos credentials available (default cache: KCM:)


debug1: No credentials were supplied, or the credentials were unavailable or inaccessible
No Kerberos credentials available (default cache: KCM:)


debug2: we did not send a packet, disable method
debug3: authmethod_lookup publickey
debug3: remaining preferred: keyboard-interactive,password
debug3: authmethod_is_enabled publickey
debug1: Next authentication method: publickey
debug1: Offering public key: /home/vincent/.ssh/id_ed25519 ED25519 SHA256:hz2ALw9+pzz6A7IW1slc4U7SXtJl1BICWeWyc/tgomU explicit
debug3: send packet: type 50
debug2: we sent a publickey packet, wait for reply
debug3: receive packet: type 51
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug2: we did not send a packet, disable method
debug3: authmethod_lookup password
debug3: remaining preferred: ,password
debug3: authmethod_is_enabled password
debug1: Next authentication method: password
vincent@10.7.1.10's password:
debug3: send packet: type 50
debug2: we sent a password packet, wait for reply
debug3: receive packet: type 52
Authenticated to 10.7.1.10 ([10.7.1.10]:22) using "password".
debug1: pkcs11_del_provider: called, provider_id = (null)
debug1: channel 0: new [client-session]
debug3: ssh_session2_open: channel_new: 0
debug2: channel 0: send open
debug3: send packet: type 90
debug1: Requesting no-more-sessions@openssh.com
debug3: send packet: type 80
debug1: Entering interactive session.
debug1: pledge: filesystem full
debug3: receive packet: type 80
debug1: client_input_global_request: rtype hostkeys-00@openssh.com want_reply 0
debug3: client_input_hostkeys: received RSA key SHA256:q7BzoPy4BErl11+JUg4VA5A6V5CXaX/XOXEyyJM0yKI
debug3: client_input_hostkeys: received ECDSA key SHA256:Q2247vJS6Bm+cJH+PcRborHIxWtuRzgvxWey54LJKyY
debug3: client_input_hostkeys: received ED25519 key SHA256:LiWk49XIVPOBhCg7+FRoMGuM+WQZInba139U+eUhqtM
debug1: client_input_hostkeys: searching /home/vincent/.ssh/known_hosts for 10.7.1.10 / (none)
debug3: hostkeys_foreach: reading file "/home/vincent/.ssh/known_hosts"
debug3: hostkeys_find: found ssh-ed25519 key at /home/vincent/.ssh/known_hosts:1
debug1: client_input_hostkeys: searching /home/vincent/.ssh/known_hosts2 for 10.7.1.10 / (none)
debug1: client_input_hostkeys: hostkeys file /home/vincent/.ssh/known_hosts2 does not exist
debug3: client_input_hostkeys: 3 server keys: 2 new, 18446744073709551615 retained, 2 incomplete match. 0 to remove
debug3: client_input_hostkeys: asking server to prove ownership for 2 keys
debug3: send packet: type 80
debug3: receive packet: type 91
debug2: channel_input_open_confirmation: channel 0: callback start
debug2: fd 3 setting TCP_NODELAY
debug3: set_sock_tos: set socket 3 IP_TOS 0x48
debug2: client_session2_setup: id 0
debug2: channel 0: request pty-req confirm 1
debug3: send packet: type 98
debug2: channel 0: request shell confirm 1
debug3: send packet: type 98
debug2: channel_input_open_confirmation: channel 0: callback done
debug2: channel 0: open confirm rwindow 0 rmax 32768
debug3: receive packet: type 81
debug3: client_global_hostkeys_private_confirm: verify RSA key 0 using default sigalg
debug3: client_global_hostkeys_private_confirm: verify ECDSA key 1 using default sigalg
Learned new hostkey: RSA SHA256:q7BzoPy4BErl11+JUg4VA5A6V5CXaX/XOXEyyJM0yKI
Learned new hostkey: ECDSA SHA256:Q2247vJS6Bm+cJH+PcRborHIxWtuRzgvxWey54LJKyY
debug3: hostkeys_foreach: reading file "/home/vincent/.ssh/known_hosts"
debug3: host_delete: ED25519 key already at /home/vincent/.ssh/known_hosts:1
Adding new key for 10.7.1.10 to /home/vincent/.ssh/known_hosts: ssh-rsa SHA256:q7BzoPy4BErl11+JUg4VA5A6V5CXaX/XOXEyyJM0yKI
Adding new key for 10.7.1.10 to /home/vincent/.ssh/known_hosts: ecdsa-sha2-nistp256 SHA256:Q2247vJS6Bm+cJH+PcRborHIxWtuRzgvxWey54LJKyY
debug1: update_known_hosts: known hosts file /home/vincent/.ssh/known_hosts2 does not exist
debug3: receive packet: type 99
debug2: channel_input_status_confirm: type 99 id 0
debug2: PTY allocation request accepted on channel 0
debug2: channel 0: rcvd adjust 2097152
debug3: receive packet: type 99
debug2: channel_input_status_confirm: type 99 id 0
debug2: shell request accepted on channel 0
Last login: Thu Jan 16 13:37:08 2025 from 10.7.1.1
[vincent@tp3 ~]$
```
4. DoT

🌞 Configurer la machine pour qu'elle fasse du DoT

```
[vincent@tp3 ~]$ sudo dnf install systemd-resolved
```
```
[vincent@tp3 ~]$ sudo systemctl start systemd-resolved
```
```
[vincent@tp3 ~]$ sudo nano /etc/systemd/resolved.conf
[Resolve]
DNS=1.1.1.1
DNSSEC=true
DNSOverTLS=yes
```
```
[vincent@tp3 ~]$ sudo ln -sf /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf
[vincent@tp3 ~]$
```
🌞 Prouvez que les requêtes DNS effectuées par la machine...

```
[vincent@tp3 ~]$ dig youtube.com

; <<>> DiG 9.16.23-RH <<>> youtube.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 25852
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;youtube.com.                   IN      A

;; ANSWER SECTION:
youtube.com.            300     IN      A       142.251.36.14

;; Query time: 48 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: Thu Jan 16 13:57:28 CET 2025
;; MSG SIZE  rcvd: 56

[vincent@tp3 ~]$
```

5. AIDE

🌞 Installer et configurer AIDE



🌞 Scénario de modification



🌞 Timer et service systemd










































