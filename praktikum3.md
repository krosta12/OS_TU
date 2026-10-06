# Praktikum 3 – Ubuntu ja LVM

**Üliõpilane:** Kostiantyn Iliushchenko  
**Kasutaja / Host:** `kostiantyn@iliushchenko26`

## 1. Paigaldus ja töölaua vahetus

* Paigaldatud **Ubuntu 26.04** virtuaalmasin (4 GB RAM, 4 CPU, 24 GB LVM ketas).
* Lisatud Guest Additions / SPICE vahendid.
* Paigaldatud **Lubuntu** töölauakeskkond:

  ```bash
  sudo apt update && sudo apt install -y lubuntu-desktop
  ```

### 📸 Tõestus 1: Lubuntu ja screenfetch

*(Pilt kogu VM aknast, kus on näha Lubuntu töölauakeskkond, `screenfetch` väljund ja kasutaja `kostiantyn@iliushchenko26`)*

## 2. LVM ümbernimetamine

* Volume Group ja Logical Volume ümbernimetamine:

  ```bash
  sudo vgrename ubuntu-vg iliushchenko-vg
  sudo lvrename iliushchenko-vg ubuntu-lv iliushchenko-lv
  ```

* Muudetud GRUB-i seadistus (`/boot/grub/grub.cfg`) ning uuendatud alglaadimise pilt:

  ```bash
  sudo update-initramfs -c -k all
  ```

## 3. LVM laiendamine uue kettaga

* Lisatud uus **3 GB** virtuaalne kõvaketas (`/dev/sdb` või UTM-is `/dev/vdb`).
* Laiendatud LVM ja failisüsteem:

  ```bash
  sudo pvcreate /dev/sdb
  sudo vgextend iliushchenko-vg /dev/sdb
  sudo lvextend -l +100%FREE /dev/iliushchenko-vg/iliushchenko-lv
  sudo resize2fs /dev/iliushchenko-vg/iliushchenko-lv
  ```

### 📸 Tõestus 2: LVM seis

*(Pilt käskude väljundist koos käsuviibaga `kostiantyn@iliushchenko26`: `sudo vgdisplay`, `sudo lvdisplay`, `lsblk`, `df -h`)*<img width="1919" height="1079" alt="Screenshot 2026-09-30 140031" src="https://github.com/user-attachments/assets/db998df1-fa0f-406d-8baa-8c24a04f26fe" />
<img width="1918" height="1079" alt="Screenshot 2026-09-30 140146" src="https://github.com/user-attachments/assets/cbe4532a-814f-499c-968e-0dd56cd92d5a" />
<img width="1917" height="1075" alt="Screenshot 2026-09-30 140241" src="https://github.com/user-attachments/assets/5d2e6843-caa7-477d-9588-23b067d1607b" />
<img width="1919" height="1079" alt="Screenshot 2026-09-30 140848" src="https://github.com/user-attachments/assets/b77df227-ee84-4143-b527-635640b5d421" />
<img width="2559" height="1439" alt="Screenshot 2026-09-30 133128" src="https://github.com/user-attachments/assets/f6d1693c-2b44-4008-a947-21aade70db96" />
