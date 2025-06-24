# ⚙️ Hyper-V

Hyper-V est l’hyperviseur natif de Microsoft pour la virtualisation sur Windows. Il permet de créer et gérer des **machines virtuelles** (VMs) sur votre poste. Cependant, pour des solutions comme VirtualBox ou VMWare Workstation Pro, toute virtualisation nestée est impossible, utile notamment pour [Proxmox](https://www.proxmox.com/), [KVM](https://linux-kvm.org/page/Main_Page) et [QEMU](https://www.qemu.org/).

---

## 📌 Prérequis

- Windows 10/11 **Pro**, **Enterprise** ou **Education**  
  (Hyper-V **n’est pas disponible** sur les éditions **Home** sans manipulation)
- Processeur 64 bits avec **SLAT** (Second Level Address Translation)
- **Virtualisation activée** dans le BIOS/UEFI
- Minimum 4 Go de RAM (8+ Go recommandé)

---

## ✅ Vérifier la compatibilité

Exécute cette commande dans PowerShell ou CMD :

```powershell
systeminfo | findstr /i "Hyper-V"
```
