# Praktikum 5: Protsessid, signaalid ja teated

Käesolevas praktikumis tutvume Linuxi protsesside, signaalide ja teadete toimimisega.

---

## Ülesanne 5-1

1. Käivitati tekstiredaktor `gedit` käsurealt.
2. Peatati protsessi töö klahvikombinatsiooniga `Ctrl+Z` (saadeti signaal `SIGTSTP`). Akna töö hangus.
3. Taastati protsessi töö, saates sellele signaali `SIGCONT`. Aken hakkab taas reageerima.

**Kasutatud käsud:**
```bash
gedit
# [Vajutatud Ctrl+Z]
kill -SIGCONT %1   # või: kill -18 <PID> / bg
```

<img width="1919" height="1079" alt="Screenshot 2026-10-17 121734" src="https://github.com/user-attachments/assets/7c42e2f7-d442-4cc1-8fea-a8e5a59e649f" />


---

## Ülesanne 5-2

1. Käivitati `gedit` taustal (`&`). SIGHUP signaali saatmisel aken sulgus.
2. Käivitati `gedit` käsuga `nohup`. SIGHUP signaali saatmisel jäi aken tööle.
3. Protsess suljeti signaaliga `SIGKILL` (`kill -9`).

**Kasutatud käsud:**
```bash
# 1. Taustal käivitamine ja SIGHUP
gedit &
ps aux | grep gedit
kill -SIGHUP <PID>
ps aux | grep gedit

# 2. nohup abil käivitamine ja SIGHUP
nohup gedit &
kill -SIGHUP <PID>
ps aux | grep gedit   # Protsess on ikka alles

# 3. Protsessi sulgemine
kill -9 <PID>
ps aux | grep gedit   # Protsess on kadunud
```

<img width="1919" height="1079" alt="Screenshot 2026-10-17 122716" src="https://github.com/user-attachments/assets/fde06c08-dba4-48d4-8aa7-8c529171923e" />

---

## Ülesanne 5-3

Käsujada, mis kuvab ainult protsesside nimed koos parameetritega, eemaldades muu info:

```bash
ps -axu | grep daemon | grep -v grep | tr -s ' ' | cut -d' ' -f11-
```

**Selgitus:**
* `tr -s ' '` – asendab mitu järjestikust tühikut ühega.
* `cut -d' ' -f11-` – eraldab väljad tühiku alusel ja kuvab alates 11. väljast kogu käsurea (programmi nime ja parameetrid).


<img width="1919" height="1079" alt="Screenshot 2026-10-17 123340" src="https://github.com/user-attachments/assets/9ab3cd3e-dded-4976-8303-ba520712dd78" />


---

## Ülesanne 5-4

IP-aadressi väljastamine `ip a` väljundist, selle salvestamine faili ja kontrollimine `ping` käsuga.

**Käsud:**
```bash
# 1. IP-aadressi kuvamine ekraanile
ip a | grep 'inet ' | grep -v '127.0.0.1' | awk '{print $2}' | cut -d'/' -f1

# 2. IP-aadressi salvestamine faili ipaddress.txt
ip a | grep 'inet ' | grep -v '127.0.0.1' | awk '{print $2}' | cut -d'/' -f1 > ipaddress.txt

# 3. Faili sisu kontrollimine ping abil
xargs -n1 ping -c 2 < ipaddress.txt
```

<img width="1919" height="1079" alt="Screenshot 2026-10-17 124143" src="https://github.com/user-attachments/assets/50bf0be7-fe63-41b8-b126-b23813aa71ca" />


---

## Ülesanne 5-5

Analüüsitud faili `teatedOut.txt` teateid:

### 1. Valitud sõnumid failist

* **Sõnum 1: `WM_MOUSEMOVE` (ID: 512 / 0x0200)**
  * **Rida failist:** `13:02:14.498,512,"WM_MOUSEMOVE",0,20971937`
  * **Tegevus:** Sõnum saadeti, kui kasutaja liigutas hiirekursorit akna alal.
  * **Parameetrid:** `wParam = 0` (ükski täiendav klahv ega hiirenupp pole all), `lParam = 20971937` (sisaldab X ja Y koordinaate akna suhtes).
  * **Allikas:** [Microsoft Learn - WM_MOUSEMOVE](https://learn.microsoft.com/en-us/windows/win32/inputdev/wm-mousemove)

* **Sõnum 2: `WM_SIZE` (ID: 5)**
  * **Rida failist:** `13:02:13.753,5,"WM_SIZE",0,28902000`
  * **Tegevus:** Sõnum saadeti akna suuruse muutmisel või avamisel.
  * **Parameetrid:** `wParam = 0` (`SIZE_RESTORED`), `lParam = 28902000` (akna uus laius ja kõrgus).
  * **Allikas:** [Microsoft Learn - WM_SIZE](https://learn.microsoft.com/en-us/windows/win32/winmsg/wm-size)

### 2. Tundmatu sõnum (`???`) ID-ga < 45000

* **Kirje failist:** `13:02:37.423,19,"???",0,0`
* **Sõnumi ID:** `19` (mis vastab teatele **`WM_CLEAR`**).
* **Selgitus:** Teade saadeti tekstivälja/sisendi kustutamise toimingul. Kuna ID 19 puudus `konst.csv` tabelis, märgiti selle nimeks `???`.
* **Allikas:** [Microsoft Learn - WM_CLEAR](https://learn.microsoft.com/en-us/windows/win32/winmsg/wm-clear)
