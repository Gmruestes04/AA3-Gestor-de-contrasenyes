# Fase 1: Anàlisi i Justificació (Document d'Informe)

## 1. Introducció i Justificació

En l'entorn corporatiu actual, la gestió deficient de les credencials d'accés representa una de les principals portes d'entrada per als cibercriminals. L'ús de contrasenyes febles, fàcils d'endevinar o la reutilització de la mateixa clau en múltiples serveis exposa l'empresa a riscos crítics de seguretat:

* **Atacs de Diccionari i Força Bruta:** Els atacants utilitzen eines automatitzades que proven milions de combinacions de paraules, caràcters i variacions en qüestió de segons. Si una contrasenya és curta o conté paraules comunes, serà compromesa ràpidament.
* **Credential Stuffing:** Quan un servei extern pateix una filtració de dades i les credencials es publiquen a la xarxa, els atacants utilitzen botnets per provar sistemàticament aquestes mateixes combinacions d'usuari/correu i contrasenya en altres plataformes corporatives (correu, VPN, panells d'administració). Si l'empleat reutilitza la clau, l'atacant aconsegueix accés immediat a la xarxa interna.
* **Falta de Traçabilitat i Control:** Si els empleats apunten les claus en fulls de càlcul no xifrats, notes adhesives o fitxers de text, l'empresa perd el control sobre qui té accés a cada recurs i s'exposa a fugues d'informació internes.

### La funció crucial d'un Gestor de Contrasenyes
Un gestor de contrasenyes corporatiu actua com una mesura de seguretat fonamental per mitigar aquests riscos:
1. **Generació de claus complexes:** Permet crear i utilitzar contrasenyes úniques, llargues i aleatòries per a cada servei sense necessitat que l'usuari les hagi de memoritzar.
2. **Emmagatzematge xifrat centralitzat:** Desa totes les credencials en un repositori protegit per algoritmes de xifratge d'alta seguretat.
3. **Reducció del Phishing:** Molts gestors s'integren amb el navegador i només emplenen automàticament les dades si el domini de la web coincideix exactament amb el desat, evitant que els empleats entreguin dades en pàgines fraudulentes.

---

## 2. Comparativa Tècnica: Bitwarden vs. KeePassXC

A continuació es presenta una anàlisi comparativa detallada entre **Bitwarden** (solució basada en el núvol) i **KeePassXC** (solució d'escriptori / local), avaluant els seus aspectes arquitectònics, de seguretat i de costos.

### Taula Comparativa

| Criteri Tècnic | Bitwarden (Alternativa Online / Núvol) | KeePassXC (Alternativa Offline / Escriptori) |
| :--- | :--- | :--- |
| **Model d'Emmagatzematge** | Centralitzat al núvol (servidors de Bitwarden o *self-hosted* en servidor propi). | Fitxer local xifrat amb extensió `.kdbx` (emmagatzemat al disc dur local o USB). |
| **Model de Seguretat i Xifratge** | Xifratge d'extrem a extrem (*End-to-End*) amb AES-256 i derivació de clau PBKDF2/Argon2. | Xifratge local amb AES-256, ChaCha20 o Twofish. Desxifratge exclusiu en RAM. |
| **Sincronització** | Automàtica i transparent entre tots els dispositius a través d'Internet. | Manual (traslladant l'arxiu `.kdbx`) o mitjançant serveis externs (Syncthing, Nextcloud). |
| **Accés Multi-dispositiu** | Molt elevat. Apps natives (Windows, macOS, Linux, iOS, Android), extensió web i portal Web Vault. | Mitjà / Baix. Apps natives d'escriptori. En mòbil requereix utilitats de tercers (KeePass2Android, Strongbox). |
| **Model de Llicència i Cost** | Open Source (GPLv3). Model *Freemium* (versió gratuïta individual i plans de pagament per a equips). | Open Source (GPLv3). 100% gratuït, sense cap mena de subscripció o versió de pagament. |
| **Independència de la Xarxa** | Requereix connexió per sincronitzar canvis (ofereix accés *offline* en mode lectura a la memòria cau). | 100% independent d'Internet. Ideal per a entorns aïllats (*Air-Gapped*). |

### Anàlisi Detallada dels Criteris Tècnics

#### 1. Model d'Emmagatzematge i Sincronització
* **Bitwarden:** La base de dades es troba centralitzada als servidors del proveïdor (o en un servidor propi si s'opta per l'opció *self-hosted*). Això permet que qualsevol canvi realitzat per un tècnic es reflecteixi a l'instant a la resta de dispositius autoritzats.
* **KeePassXC:** Totes les dades es guarden en un únic fitxer amb extensió `.kdbx`. La sincronització entre diferents equips depèn directament de l'usuari. Si dos tècnics modifiquen la mateixa base de dades local simultàniament, es poden produir conflictes de versions i pèrdua d'informació si no es gestiona acuradament.

#### 2. Model de Seguretat i Xifratge
* **Bitwarden:** Implementa una arquitectura de **Zero-Knowledge** (Coneixement Zero). Les dades es xifren i desxifren a nivell de client utilitzant AES-256. La contrasenya mestra mai s'envia als servidors de Bitwarden, per la qual cosa, fins i tot en el cas d'una filtració als seus servidors, les dades continuen sent inaccessibles sense la clau mestra.
* **KeePassXC:** Proporciona una superfície d'atac pràcticament nul·la pel que fa a la xarxa, ja que el programari no realitza connexions jueves directes. La seguretat depèn íntegrament del xifratge del fitxer `.kdbx` i de la seguretat física o lògica de l'equip on està instal·lat.

#### 3. Accés Multi-dispositiu i Usabilitat
* **Bitwarden:** Ofereix una integració excel·lent en entorns heterogenis. Les extensions per a navegadors (Chrome, Firefox, Edge) faciliten l'emplenament automàtic de credencials a aplicacions web de l'empresa sense necessitat de copiar i enganxar manualment.
* **KeePassXC:** Excel·leix en entorns d'escriptori (Windows, Linux, macOS), però l'accés des de dispositius mòbils requereix confiar en aplicacions desenvolupades per tercers no oficials, reduint la senzillesa d'ús per a l'usuari final.

#### 4. Model de Llicència i Cost
* **Bitwarden:** Compta amb una versió gratuïta molt completa per a ús personal, però per a entorns corporatius que requereixin organitzacions, compartir carpetes de credencials entre equips i auditories d'accés, s'ha de contractar un pla empresarial (*Enterprise/Teams*).
* **KeePassXC:** Programari 100% lliure i gratuït sense cap cost de llicenciament, reduint a zero el cost directe de programari per a l'organització.

---

## 3. Avantatges i Inconvenients (Online vs. Offline)

### Model Online / Núvol (Bitwarden)
* **Avantatges:**
  * **Usabilitat elevada:** Alta facilitat d'accés des de qualsevol lloc i dispositiu (web, mòbil, extensió).
  * **Treball en equip:** Permet compartir credencials i carpetes entre membres de l'equip de forma controlada.
  * **Sincronització automàtica:** Evita el risc de treballar amb bases de dades desactualitzades.
  * **Backup gestionat:** Les dades estan protegides al núvol davant de fallades del maquinari local.
* **Inconvenients:**
  * **Dependència de la xarxa:** Es requereix connexió a Internet per a la sincronització de noves dades.
  * **Risc de tercers:** Encara que s'utilitza xifratge *Zero-Knowledge*, les dades estan allotjades en infraestructura externa.

### Model Offline / Escriptori (KeePassXC)
* **Avantatges:**
  * **Control total de les dades:** La base de dades `.kdbx` està sota el domini absolut de l'empresa.
  * **Màxima privacitat:** Cap dada s'envia a servidors externs ni viatja per Internet.
  * **Ideal per a entorns aïllats:** Funciona perfectament en màquines o xarxes sense accés a la xarxa (*Air-Gapped*).
  * **Cost zero:** Absència total de tarifes de subscripció o llicenciament.
* **Inconvenients:**
  * **Gestió manual de Backups:** Si l'usuari no fa còpies de seguretat del fitxer `.kdbx` i el disc dur s'espatlla, les dades es perden irrecuperablement.
  * **Sincronització complexa:** Dificultat per compartir actualitzacions de contrasenyes en temps real entre diferents tècnics.
  * **Menys còmode en mòbils:** Requereix utilitzar aplicacions de tercers i moure el fitxer manualment.

---

## 4. Recomanació

Com a conclusió de l'informe tècnic, es recomana la implementació de **Bitwarden** com a gestor de contrasenyes corporatiu per al personal tècnic de l'empresa.

### Justificació de la meva elecció:
1. **Dinamisme de l'Equip Tècnic:** L'equip de sistemes i xarxes opera habitualment des de diferents entorns (servidors, portàtils de treball, dispositius mòbils i entorns web). La sincronització automàtica i multi-dispositiu de Bitwarden garanteix l'accés immediat a les credencials sense interrompre el flux de treball.
2. **Seguretat Garantida (Zero-Knowledge):** Tot i ser una solució al núvol, la seva arquitectura assegura que només el personal autoritzat amb la contrasenya mestra pugui desxifrar la informació, mantenint un nivell de seguretat equivalent al model offline.
3. **Gestió d'Equips i Col·laboració:** Bitwarden permet crear orgs corporatives i compartir credencials de servidors o serveis comuns entre tècnics de forma segura i auditable, evitant l'enviament de claus per canals insegurs com xats o correus electrònics.

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