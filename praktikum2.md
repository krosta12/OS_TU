# Linuxi käsurea praktikum - Aruanne

Lühike ülevaade praktikumis teostatud Linuxi käsurea ülesannetest ja kasutatud käskudest.

---

### 1. Faili sisu kuvamine (`/etc/hosts`)
Kuvasin faili `/etc/hosts` sisu käsureale.
```bash
cat /etc/hosts
```

---

### 2. Kataloogide loomine
Lõin kasutaja kodukataloogi uue kataloogi, mille nimi sisaldab väiketähte, numbrit, tühikut, võrdlusmärki ja lauselõpumärki.
```bash
mkdir "/home/user/a1 > ."
```

---

### 3. Failide otsimine nime järgi
Otsisin juurkataloogist (`/`) ja selle alamkataloogidest absoluutse teega faili, mille nimi lõpeb sõnaga `hidden_secret`.
```bash
find / -name "*hidden_secret" 2>/dev/null
```

---

### 4. Faili otsimine sisu järgi
Otsisin `/var` kataloogist ja selle alamkataloogidest faili, mis sisaldab teksti `"Sudo password"`.
```bash
grep -rnw '/var' -e 'Sudo password' 2>/dev/null
```

---

### 5. Tarkvara paigaldamine ja asukoha leidmine
Paigaldasin paketi `nano` ja tuvastasin selle käivitatava faili asukoha süsteemis.
```bash
sudo apt update && sudo apt install -y nano
which nano
```

---

### 6. Faili õiguste muutmine
Lõin faili `test_file`, lisasin sinna oma nime ning määrasin õigused `660` (omanikule ja grupile lugemine/kirjutamine, teistele juurdepääs puudub).
```bash
echo "Eesnimi Perenimi" > /home/user/test_file
chmod 660 /home/user/test_file
ls -la /home/user/test_file
```

---

### 7. Faili allalaadimine ja sõnade loendamine
Laadisin veebist alla tekstifaili ja kuvasin ainult selles sisalduvate sõnade arvu.
```bash
curl -s https://raw.githubusercontent.com/eistre/terminal/master/resources/tammsaare.txt | wc -w
```

---

### 8. Torud (Pipes)
Kuvasin käsuga `df -h` süsteemi kettakasutuse, filtreerides väljundist välja ainult veeru `Filesystem`.
```bash
df -h | awk '{print $1}'
```

---

### 9. Kataloogi kustutamine
Kustutasin rekursiivselt kataloogi `/home/user/.temporary` koos kogu selle sisuga.
```bash
rm -rf /home/user/.temporary
```

---

### 10. Töötavad protsessid
Kuvasin kõik süsteemis parajasti töötavad protsessid.
```bash
ps aux
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8e450c05-2326-49ae-aafa-609832cab33c" />
