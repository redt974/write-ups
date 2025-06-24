## 🔢 **Méthode générale pour calculer un masque réseau**

1. **Nombre d’hôtes nécessaires ➝ déterminer les bits nécessaires pour l’hôte :**
    
    - Trouver la puissance de 2 juste supérieure ou égale au nombre d'hôtes + 2 (réseau + broadcast).
        
    - Exemple : pour 62 hôtes ➝ 2⁶ = 64 ➝ donc 6 bits pour les hôtes.
        
2. **Calcul du préfixe CIDR :**
    
    - 32 bits totaux - bits pour hôtes = nombre de bits pour le réseau ➝ /prefix.
        
    - Exemple : 32 - 6 = /26.
        
3. **Masque en décimal :**
    
    - Convertir le préfixe en notation décimale (ex: /26 ➝ 255.255.255.192).
        
4. **Plage d’adresses :**
    
    - Adresse réseau = première adresse.
        
    - Adresse de broadcast = dernière adresse de la plage.
        
    - IP utilisables = entre les deux.
        

---

## 🧾 **Tableau synthétique des classes d’adresses IP**

|Classe|Plage d’adresses IP|Masque par défaut|CIDR|IP possibles|IP utilisables|Adresses privées|
|---|---|---|---|---|---|---|
|A|0.0.0.1 – 126.255.255.254|255.0.0.0|/8|16 777 216|16 777 214|10.0.0.0 – 10.255.255.255|
|B|128.0.0.1 – 191.255.255.254|255.255.0.0|/16|65 536|65 534|172.16.0.0 – 172.31.255.255|
|C|192.0.0.1 – 223.255.255.254|255.255.255.0|/24|256|254|192.168.0.0 – 192.168.255.255|
|D|224.0.0.0 – 239.255.255.255|(Multicast)|—|—|—|—|
|E|240.0.0.0 – 255.255.255.255|(Expérimental)|—|—|—|—|


---

## 📊 **Tableau des cas de subnetting personnalisés**

| Contexte (réseau de base) | Hôtes souhaités | Bits hôtes | CIDR | Masque          | IP possibles | IP utilisables | Plage d’adresses (exemples)           |
| ------------------------- | --------------- | ---------- | ---- | --------------- | ------------ | -------------- | ------------------------------------- |
| 10.0.0.0/19               | 8000            | 13         | /19  | 255.255.224.0   | 8192         | 8190           | 10.0.0.0 – 10.0.31.255                |
| 192.168.0.0/25            | 64              | 7          | /25  | 255.255.255.128 | 128          | 126            | 192.168.0.0 – 192.168.0.127           |
| 172.16.0.0/22             | 1000            | 10         | /22  | 255.255.252.0   | 1024         | 1022           | 172.16.0.0 – 172.16.3.255             |
| 10.0.0.0/24               | 250             | 8          | /24  | 255.255.255.0   | 256          | 254            | 10.0.0.0 – 10.0.0.255                 |
| 172.16.0.0/25             | 120             | 7          | /25  | 255.255.255.128 | 128          | 126            | 172.16.0.0 – 172.16.0.127             |
| 10.0.0.0/18               | 16000           | 14         | /18  | 255.255.192.0   | 16384        | 16382          | 10.0.0.0 – 10.0.63.255                |
| 192.164.10.0/26           | 32              | 6          | /26  | 255.255.255.192 | 64           | 62             | 192.164.10.0 – 192.164.10.63          |
| 172.16.0.0/19             | 7650            | 13         | /19  | 255.255.224.0   | 8192         | 8190           | 172.16.0.0 – 172.16.31.255            |
| 172.21.0.0/26             | 40              | 6          | /26  | 255.255.255.192 | 64           | 62             | 172.21.0.0 – 172.21.0.63              |
| 10.0.0.0/17               | 24000           | 15         | /17  | 255.255.128.0   | 32768        | 32766          | 10.0.0.0 – 10.0.127.255               |
| 10.0.0.0/23               | 500             | 9          | /23  | 255.255.254.0   | 512          | 510            | 10.0.0.0 – 10.0.1.255                 |
| 192.168.90.0/30           | 2               | 2          | /30  | 255.255.255.252 | 4            | 2              | 192.168.90.0 – 192.168.90.3 (liaison) |

---

Chaque ligne représente un cas typique de subnetting avec :

- **l’IP de base** (souvent privée),
    
- **le besoin en hôtes**,
    
- **la conversion en bits**, puis le **/CIDR** et **masque correspondant**,
    
- **la plage résultante** (adresse réseau → broadcast).
    

