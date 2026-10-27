# Praktikum 6 – Failiõigused Linuxis

## 6-1. Faili lugemine ja kustutamine

**a)** Faili `/tmp/kaust/minufail.txt` lugemiseks on vaja kataloogile `/tmp/kaust` läbimisõigust (`x`) ja failile lugemisõigust (`r`).

**b)** Faili kustutamiseks on vaja kataloogi kirjutamis- (`w`) ja läbimisõigust (`x`). Faili enda õigused ei määra, kas seda saab kustutada.

## 6-2. Skripti käivitamine

Skriptil peab olema käivitamisõigus (`x`) ning interpretaatoril peab olema võimalik skripti lugeda (`r`). Omanikule saab õigused anda käsuga `chmod u+rx skript.sh`.

## 6-3. Privaatne kasutajagrupp ja umask

Privaatse kasutajagrupi korral kuuluvad kasutaja loodud failid vaikimisi tema enda gruppi. `umask 022` eemaldab grupilt ja teistelt kirjutamisõiguse, `umask 002` jätab grupile kirjutamisõiguse.

## 6-4. Faili lugemisõigused

Kasutaja, kes kuulub gruppi `majasisene`, vajab failile grupi lugemisõigust (`g+r`) ja kataloogile grupi läbimisõigust (`g+x`). Kataloogi sisu loetlemiseks on vaja ka kataloogi lugemisõigust (`g+r`).

## 6-5. Setuid

Setuid-bitt võimaldab käivitataval programmil töötada faili omaniku efektiivse kasutaja-ID-ga. Nii saab programm lugeda faili `hinded.txt` ja kuvada Juku hinded, kuigi tavakasutaja ei saa algset faili lugeda.

**Ekraanipilt:** faili `hinded.txt` ja programmi `hindedJukul` õigused ning programmi väljund.
<img width="1919" height="1079" alt="Screenshot 2026-10-27 124940" src="https://github.com/user-attachments/assets/3438e6bd-489b-4e6e-b1fd-7ef47c7db307" />


## 6-6. Setuid kasutamine ja riskid

Setuid on kasulik programmides, mis peavad tegema piiratud toiminguid kõrgemate õigustega, näiteks `passwd`. Vigane või ebaturvaline setuid-programm võib anda ründajale liigsed õigused.

## 6-7. Sticky bit

Sticky bitiga kataloogis (`1777`) saab faili kustutada faili omanik, kataloogi omanik või `root`. Teised kasutajad ei saa teise kasutaja faili kustutada.

## 6-8. ACL

ACL võimaldab anda õigusi konkreetsetele kasutajatele või gruppidele lisaks tavalistele failiõigustele. `getfacl` kuvab ACL-i ning `ls -l` õiguste lõpus olev `+` näitab, et failil või kataloogil on täiendav ACL.

**Ekraanipilt:** `getfacl` väljund.
<img width="1919" height="1079" alt="Screenshot 2026-10-27 125602" src="https://github.com/user-attachments/assets/4ed2f237-87b3-4886-a57b-800c67a4b9e5" />


## 6-9. Muutumatu fail

Käsk `chattr +i fail` muudab faili muutmatuks. Faili ei saa muuta ega kustutada enne, kui atribuut eemaldatakse käsuga `sudo chattr -i fail`.

**Ekraanipilt:** `lsattr` väljund ja kustutamise veateated.
<img width="1919" height="1079" alt="Screenshot 2026-10-27 130429" src="https://github.com/user-attachments/assets/c1bed54e-d83a-456d-b864-18bfe16ff9fb" />
