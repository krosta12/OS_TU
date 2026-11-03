# Praktikum 7: Haakimine - Aruanne

## Ülesanne 7-1: Miks uued andmekandjad vajavad praktikumis sooritatud lähtestamist?
Uued kettad ei sisalda partitsioonitabelit ega metaandmeid, mistõttu operatsioonisüsteem ei oska andmeplokke adresseerida. Lähtestamine loob esmase struktuuri (GPT/MBR), mis on vajalik loogiliste mahtude ja failisüsteemi loomiseks.

## Ülesanne 7-2: GPT eelised MBR-i ees
1. **Suurem mahutavus:** Toetab kettaid üle 2 TB (kuni 8 ZB), erinevalt MBR-i 2 TB piirangust.
2. **Varukoopia:** GPT salvestab partitsioonitabeli koopia ketta lõppu, mis tagab turvalisuse rikke korral.
3. **Rohkem partitsioone:** Võimaldab luua kuni 128 primaarset partiisiooni (MBR-is piiriks 4).
4. **Terviklikkuse kontroll:** Kasutab CRC32 kontrollsummasid vigade tuvastamiseks ja parandamiseks.

## Ülesanne 7-3: Võrguketta haakimine Windowsis
[https://kodu.ut.ee/~kostiantyn/opsys/hdd.png](https://kodu.ut.ee/~kostiantyn/opsys/hdd.png)

## Ülesanne 7-4: Kaugkataloogi sisu Ubuntus
<img width="1919" height="1079" alt="Screenshot 2026-11-03 163510" src="https://github.com/user-attachments/assets/ffd50d4c-4f0d-48b1-a050-5acacb16ba1c" />


## Ülesanne 7-5: Mount-käsu parameetrid
* `-o ro` — haagib andmekandja ainult lugemiseks (read-only), kaitstes andmeid muutmise eest.
* `-t auto` — käskib süsteemil failisüsteemi tüüp (nt NTFS, VFAT) automaatselt tuvastada.

## Ülesanne 7-6: Automaatse tüübi asendus
Ubuntu asendas parameetri `auto` konkreetse tuvastatud failisüsteemi väärtusega (näiteks `ntfs3` või `vfat`).

## Ülesanne 7-7: Püsiv haakimine (/etc/fstab)
<img width="1919" height="1079" alt="Screenshot 2026-11-03 163741" src="https://github.com/user-attachments/assets/46561dbf-8ff8-4aef-b43a-451f8c663232" />
