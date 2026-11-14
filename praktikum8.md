# Praktikum 8 — RAID ja andmete varundamine

**Kostiantyn Iliushchenko** · VirtualBox 7.2.16 · Windows 11 25H2 (`OS-Iliushchenko-W11`) · Ubuntu 26.04 (`OS-Iliushchenko-Ubuntu26`)

## 8-1 RAID 1 Windowsis

* Lisatud 2×1 GB ketast, mõlemad lähtestatud MBR-ina.
* `diskpart`: `K:` NTFS, silt `Iliushchenko`; `convert dynamic` + `add disk=3` → peegel.
* Fail `K:\kostiantyn.txt`: **Operatsioonisüsteemid 2026 oluline fail**.
* Rike: teine ketas offline → volume `Nurjunud liiasus`, ketas `Puuduv`, `K:` jäi loetavaks.

<img width="1600" height="900" alt="8-1_windows_failed_redundancy" src="https://github.com/user-attachments/assets/d99ea345-cbf3-4331-9084-7cd5a9e17992" />


## 8-2 RAID 1 Ubuntus

* 2×1,5 GB ketast (`sdc`, `sdd`), `fdisk` partitsioonitüüp `fd`.
* `mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdc1 /dev/sdd1` → `mkfs.ext4` → `/mnt/raid1_ketas`.
* Püsivus: `/etc/fstab` (`nofail`), `/etc/mdadm/mdadm.conf` (`ARRAY /dev/md0`), `update-initramfs -u`.
* Rike: `[2/1] [U_]`; `nofail` tõttu emergency mode'i ei läinud. Asendusketas + `mdadm --add` → `[2/2] [UU]`.

<img width="1024" height="768" alt="8-2_ubuntu_raid1_degraded" src="https://github.com/user-attachments/assets/b22ab360-ff0e-4816-b173-0acb60277262" />
<img width="1024" height="768" alt="8-2_ubuntu_raid1_restored" src="https://github.com/user-attachments/assets/3496222d-3385-4d8e-a13f-9f50158a1552" />


## 8-3 Nextcloud Windowsis

Fail `nextcloud_test_kostiantyn.txt` kaustas `UT/OS/Operatsioonisüsteemid_2026`, jagatud **Alo Peets**iga (`Can edit`).
<img width="1919" height="1079" alt="Screenshot 2026-11-14 142644" src="https://github.com/user-attachments/assets/40407be4-27e5-44c5-ab8d-9aca4e65b2a5" />

## 8-4 Nextcloud Ubuntus

`nextcloud-desktop` 4.0.6; fail `~/nextcloud/UT/OS/Operatsioonisüsteemid_2026/` (SSO-tõttu paigutatud sünkroonkausta käsitsi).

<img width="1024" height="768" alt="8-4_ubuntu_nextcloud_file_properties" src="https://github.com/user-attachments/assets/e035dbbd-aaa3-4ee3-85c6-88f715cad22a" />


## 8-5 OneDrive

OneDrive'i klient Windowsis TÜ Microsoft 365 kontoga. Ekraanipilt: `Settings → Account`.

**Järeldus:** RAID 1 annab liiasuse, mitte varunduse; `nofail` muudab degradeeritud massiivi käivitumist.

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/faeb71f0-6356-47fc-8ebb-e17cb5528d1f" />
