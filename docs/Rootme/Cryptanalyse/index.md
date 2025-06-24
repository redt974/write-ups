# 🔐 Cryptanalyse – Write-Ups

Bienvenue dans la section **cryptanalyse**, où je documente la résolution de challenges liés à la cryptographie :

- Substitution, chiffrement classique (Caesar, Vigenère…)
- XOR, Base64, Base32, rot13, etc.
- RSA, padding oracle, factorisation
- Stéganographie orientée bits
- Et plus encore !

---

## 🗂️ Liste des challenges

| Nom du challenge                  | Type de chiffrement     | Lien |
|----------------------------------|--------------------------|------|
| [Hash - DCC2](Hash%20-%20DCC2/Hash%20-%20DCC2.md)           | César (shift simple)        | ✔️ |
| ...                              | ...                      | ...  |

---

## 📌 Recommandations

- Utilisez des outils comme `CyberChef`, `Cryptool`, `hash-identifier`, ou `gchq/CyberChef` en ligne.
- Essayez d’automatiser les attaques via Python et la lib `pwntools` ou `sympy` pour RSA.
- Toujours vérifier : encodage ≠ chiffrement.

---

## 🛠️ Scripts utiles

📁 `scripts/crypto/` — contient des snippets ou mini scripts pour :
- Détection automatique de chiffrements
- Brute force de Vigenère avec dictionnaire
- Cracking RSA `n = p*q` faibles
