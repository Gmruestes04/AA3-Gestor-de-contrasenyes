# Activitat: Gestió de Contrasenyes 

## Fase 1: Anàlisi i Justificació

### 1. Introducció i Justificació
L'ús de contrasenyes febles o repetides és un dels punts més vulnerables a qualsevol empresa:
* **Atacs de diccionari:** Software automatitzat que prova milers de paraules per segon. Si la clau és simple, la treuen al moment.
* **Credential stuffing:** Si filtren la clau d'un servei extern i l'empleat la reutilitza a l'empresa, els atacants entren directament als nostres sistemes (correu, VPN, etc.).
* **Falta de control:** Tenir claus apuntades en notes, fulls de càlcul o arxius de text fa que qualsevol les pugui veure i es perdi la traçabilitat.

**Per què fa falta un gestor?**
1. Permet crear claus complexes, llargues i úniques per a cada servei sense haver-les de recordar.
2. Centralitza i xifra tota la informació sota una sola contrasenya mestra.
3. Evita el *phishing*, ja que les extensions de navegador només omplen les dades si el domini de la web coincideix exactament.

---

### 2. Comparativa Tècnica: Bitwarden vs. KeePassXC

| Criteri Tècnic | Bitwarden (Online / Núvol) | KeePassXC (Offline / Escriptori) |
| :--- | :--- | :--- |
| **Emmagatzematge** | Centralitzat al núvol (servidors propis o de Bitwarden). | Fitxer local xifrat (`.kdbx`) al disc o USB. |
| **Xifratge i Seguretat** | Extrem a extrem (*Zero-Knowledge*) amb AES-256. | Local amb AES-256 / ChaCha20. Desxifrat només en RAM. |
| **Sincronització** | Automàtica entre tots els dispositius. | Manual (movent el fitxer) o amb eines externes (Nextcloud/Syncthing). |
| **Multi-dispositiu** | Molt bona (Windows, Linux, Mac, iOS, Android, navegadors). | Acceptable a PC/Linux/Mac; en mòbil calen eines de tercers. |
| **Llicència i Cost** | Open Source (GPLv3). Model *Freemium* (plans per a equips). | Open Source (GPLv3). 100% gratuït sense opcions de pagament. |
| **Dependència de Xarxa** | Cal connexió per sincronitzar (ofereix lectura *offline*). | 100% independent d'Internet (ideal per a entorns aïllats). |

---

### 3. Avantatges i Inconvenients

#### Bitwarden (Online)
* **Pros:** Molt fàcil d'usar, sincronització automàtica i permet compartir carpetes de claus entre l'equip tècnic.
* **Contres:** Depèn de tenir Internet per sincronitzar nous canvis i les dades es guarden en servidors externs.

#### KeePassXC (Offline)
* **Pros:** Control absolut de l'arxiu `.kdbx`, cap dada surt a Internet i és 100% de franc.
* **Contres:** Si el disc s'espatlla i no hi ha backup es perd tot, i la sincronització entre tècnics o amb el mòbil és manual.

---

### 4. Recomanació
Es recomana **Bitwarden** per al personal tècnic. La sincronització automàtica entre diferents equips i la facilitat per compartir credencials corporatives de manera segura superen el model local, mantenint una seguretat excel·lent gràcies al xifratge de coneixement zero (*Zero-Knowledge*).

---
# Fase 2: Guia d'Ús Tècnica (Manual Operatiu - Bitwarden)

Aquest manual explica pas a pas com instal·lar, configurar i utilitzar **Bitwarden** com a gestor de contrasenyes corporatiu per a l'equip tècnic.

---

## 1. Instal·lació i Configuració Inicial

### 1.1 Descàrrega i instal·lació de l'aplicació d'escriptori
1. Obre el navegador a la màquina virtual (Windows 11) i entra a la pàgina oficial: `https://bitwarden.com/download/`.
2. Descarrega l'instal·lador per a **Windows**.
3. Executa el fitxer descarregat (`Bitwarden-Installer.exe`) i segueix els passos de l'assistent d'instal·lació per defecte.

![alt text](<Captura de pantalla 2026-11-06 181328.png>)

### 1.2 Creació del compte i Contrasenya Mestra
1. Un cop instal·lat, obre l'aplicació de Bitwarden i fes clic a **Crear compte** (*Create Account*).
2. Introdueix el teu correu electrònic corporatiu.
3. Defineix la teva **Contrasenya Mestra** (*Master Password*). 
   > ⚠️ **Important:** Aquesta contrasenya és l'única clau que desxifra totes les altres. Ha de ser llarga (mínim 14-16 caràcters), combinant majúscules, minúscules, números i símbols. Si la perds, no es podrà recuperar el compte.
4. (Opcional) Afegeix una pista per a la contrasenya i fes clic a **Crear compte**.

![alt text](<Captura de pantalla 2026-11-06 181513.png>)

---

## 2. Generació de Contrasenyes Segures

Per evitar crear contrasenyes febles, utilitzarem el generador automàtic integrat a Bitwarden:

1. Dins de l'aplicació o l'extensió, fes clic a la icona de **Generador** (*Generator*).
2. Configura els paràmetres recomanats per a l'empresa:
   * **Tipus:** Contrasenya (*Password*).
   * **Longitud:** Mínim 16 caràcters.
   * **Opcions actives:** Majúscules (`A-Z`), Minúscules (`a-z`), Números (`0-9`) i Símbols (`!@#$%^&*`).
3. Fes clic a **Generar contrasenya** o a la icona de copiar per fer servir la clau aleatòria creada.

![alt text](<Captura de pantalla 2026-11-06 182000.png>)

---

## 3. Exemples d'Ús i Emplenament Automàtic

### 3.1 Desar una credencial de correu electrònic
1. Vegues a l'apartat **El meu repositori** (*Vault*) i fes clic al botó **+ (Afegir element)**.
2. Emplena els camps bàsics:
   * **Nom:** Correu Corporatiu / Gmail Enterprise.
   * **Nom d'usuari:** `usuari@empresa.com`.
   * **Contrasenya:** Utilitza el generador integrat per posar una clau segura.
   * **URI / Web:** `https://mail.google.com` (o la URL del webmail).
3. Fes clic a **Desar** (*Save*).

![alt text](<Captura de pantalla 2026-11-06 183533.png>)

### 3.2 Desar una credencial d'una aplicació o servei web
1. Prem de nou el botó **+ (Afegir element)**.
2. Completa les dades del servei intern o extern (per exemple, panell d'administració o un servei Cloud):
   * **Nom:** Panell Servidor Web / Nextcloud.
   * **Nom d'usuari:** `admin_tecnic`.
   * **Contrasenya:** Clau generada de 16+ caràcters.
   * **URI 1:** `https://panell.empresa.local`.
3. Fes clic a **Desar**.

![alt text](<Captura de pantalla 2026-11-06 183753.png>)

---

## 4. Gestió de Còpies de Seguretat (Backup)

### 4.1 Exportació de la base de dades de contrasenyes
És fonamental tenir una còpia de seguretat de les dades en cas d'emergència:

1. Dins de l'aplicació de Bitwarden, ves a **Ajustos** (*Settings*) > **Exportar repositori** (*Export Vault*).
2. Selecciona el format d'exportació:
   * **JSON xifrat (*Encrypted JSON*):** **Recomanat**. Manté el xifratge de les teves dades protegit amb la teva clau de compte o una contrasenya personalitzada.
   * **CSV / JSON plà:** No recomanat, ja que deixa les contrasenyes en text pla sense xifrar.
3. Introdueix la teva Contrasenya Mestra per confirmar la descàrrega del fitxer.

![alt text](<Captura de pantalla 2026-11-06 184026.png>)

### 4.2 Bona pràctica per emmagatzemar la còpia de seguretat
Per garantir la seguretat del backup descarregat:

* **Unitat USB xifrada:** Copia el fitxer d'exportació en un llapis USB xifrat amb **BitLocker** (en Windows) o **LUKS** (en Linux).
* **Emmagatzematge al núvol segur:** Si es desa al núvol, s'ha d'assegurar que el fitxer exportat estigui prèviament xifrat (amb el format JSON xifrat de Bitwarden o utilitzant eines com **VeraCrypt** o 7-Zip amb contrasenya AES-256).
* **Guardat físic:** Guarda el llapis USB en una caixa forta o armari tancat amb clau a l'oficina.