# 1
<img width="1919" height="1079" alt="Screenshot 2026-10-10 134711" src="https://github.com/user-attachments/assets/ddfa031e-8053-43e8-8f23-c70896b4a6e2" />

#2
<img width="1919" height="1079" alt="Screenshot 2026-10-10 135552" src="https://github.com/user-attachments/assets/d8553a09-4d15-4a39-9f2b-c3337a3f8fd7" />
<img width="1919" height="1079" alt="Screenshot 2026-10-10 151710" src="https://github.com/user-attachments/assets/2f6fcd86-8b89-430b-ac07-5fed10044361" />
#3
<img width="1919" height="1079" alt="Screenshot 2026-10-10 140323" src="https://github.com/user-attachments/assets/0b6cd039-2840-412c-af14-a22d0881ca6f" />
#4
Võrreldes tavakasutaja, administraatori ja SYSTEM konto privileege, on näha järgmised erinevused:

Tavakasutaja privileegide nimekiri on piiratud ning peaaegu kõik olulised õigused on olekus Disabled. See hoiab ära olukorra, kus tavakasutaja saaks süsteemi tööd või turvalisust ohtu seada.

Administraatori õigustes on enamik privileege olemas, kuid tavarežiimis hoiab UAC neid piiratuna, kuni tegevust eraldi ei kinnitata.

SYSTEM (nt authority\system) on operatsioonisüsteemi tuuma (kerneli) tase, millel on piiramatud ja kõrgeimad õigused. Erinevalt administraatorist on SYSTEM kontol kriitilised privileegid (nt SeTcbPrivilege, SeDebugPrivilege, SeLockMemoryPrivilege) vaikimisi aktiivsed (Enabled).

Tegevused, mille jaoks on vaja SYSTEMi õigusi (administraatori õigustest ei piisa):

Ligipääs kaitstud registriharudele: Registri võtme HKEY_LOCAL_MACHINE\SAM lugemine ja muutmine (kus hoitakse kasutajakontode paroolide räsisid). Administraatoril puudub sellele otse ligipääs ilma omanikuõiguste manuaalse ülevõtmiseta.

Süsteemsete teenuste ja draiverite haldus: Madala taseme süsteemiteenuste (nt Volume Shadow Copy või turvatarkvara sisekomponentide) protsesside mälu lugemine ja silumine (debug), mida operatsioonisüsteem kaitseb isegi administraatori eest.

#5
<img width="774" height="529" alt="Screenshot 2026-10-10 142116" src="https://github.com/user-attachments/assets/4bd892b3-0130-4493-a803-395a61cf257d" />

#6
Microsofti arvates peaksin Kontokaitse alamseadistuse juures aktiveerima Microsofti konto: Suurema turvalisuse huvides ja muude eeliste kasutamiseks logige sisse Microsofti kontoga.

#7
<img width="1919" height="1079" alt="Screenshot 2026-10-10 144203" src="https://github.com/user-attachments/assets/21b72062-b366-4ac4-bc8f-1de57f0608da" />

#8
<img width="1919" height="1076" alt="Screenshot 2026-10-10 145333" src="https://github.com/user-attachments/assets/9fc20d2f-d0ad-4063-a211-a6e4098c0f59" />

#9
<img width="1919" height="1079" alt="Screenshot 2026-10-10 145939" src="https://github.com/user-attachments/assets/ef02cd44-19bb-49f8-952c-8ff9c0ad637f" />

#10
<img width="1919" height="1079" alt="Screenshot 2026-10-10 151053" src="https://github.com/user-attachments/assets/4bcc43a9-0f41-43e5-8d3a-4911e3add723" />
