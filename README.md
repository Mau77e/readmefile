# README #

#### Deze README goed lezen

==========================================================================================================
# Firewallbeleid
==========================================================================================================

### Q1
##### 1. De firewalls moeten zodanig ingericht zijn dat alleen het webverkeer van het internet naar de server wordt doorgelaten. 
### A1
1. Alles dicht behalve port 80 en port 443

==========================================================================================================

### Q2
##### 2. Er moet een policy zijn ingesteld om wijzigingen op de configuratie van firewalls te monitoren en er moet een specifiek logboek voor zijn aangemaakt.
### A2
2. Dit kun je vinden onder: Group Policy Management via de Server manager
klik op Forest: -> je domain -> Starter GPO’s -> Rechtermuisknop en dan NEW
Kies hier voor Group Policy Reporting Firewall Ports

### extra info:
als de Group Policy Manager er niet is: https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265969(v=ws.11)

==========================================================================================================

### Q3
##### 3. Services en applicaties die niet het bedrijfsdoel dienen, moeten worden geblokkeerd. 
### A3
kijk hier: https://www.technipages.com/prevent-users-from-running-certain-programs

==========================================================================================================

### Q4
##### 4. Beheer op afstand van de firewalls moet alleen mogelijk zijn vanuit het LAN. 
### A4
kijk hier: https://softwarekeep.com/help-center/how-to-enable-remote-desktop-on-windows
let op het vinkje: Allow connections only from computers running Remote Desktop with Network Level Authentication

gpedit.msc in de command box CMD.exe = local group policy editor
ga naar Remote Desktop Services -> Connections hier kun je hetzelde instellen

Ook de firewall moet ingericht worden zodat poort 3389 (RDP) alleen benaderbaar is vanaf het lan dus IP range xxx.xxx.xxx.x/24 

voorbeelden zie je hier: https://security.stackexchange.com/questions/34709/enable-rdp-for-internal-network-only

==========================================================================================================
# Toegangsbeheerbeleid
==========================================================================================================

### Q1
##### 1.	Het wachtwoord moet bestaan uit minimaal acht (8) karakters en maximaal vijftien (15) karakters.

a.	Letters: alleen letters a-z en A-Z zonder accenten worden geaccepteerd.
b.	Het moet tenminste één cijfer bevatten. Cijfers: 0 t/m 9
c.	Het moet tenminste één hoofdletter bevatten.
d.	Het moet tenminste één van de tekens bevatten. Tekens: ! % # ( ) _ + - \ < > /= { } [ ] |
e.	Gebruikersnaam en wachtwoord mogen niet hetzelfde zijn.
f.	Een nieuw wachtwoord mag niet hetzelfde zijn als de zes wachtwoorden die daarvoor zijn gebruikt.

### A1

ik ga er even vanuit dat je dit moet doen op de Active Directory gezien iedereen daarmee inlogd in het domein

hier kun je vinden hoe: http://dalaris.com/how-to-change-password-complexity-policy-on-a-windows-server/

==========================================================================================================

### Q2

##### 2.	Inloggen in de bedrijfsnetwerk moet alleen worden toegestaan binnen bepaalde tijdsvensters:
a.	Inloggen voor domain users op de gespecificeerde tijden
i.	Maandag tot en met vrijdag tussen 7.00 uur en 21.00 uur
ii.	Op zaterdag van 7.00 uur tot 11.00 uur
iii.	Op zondag geen toegang

### A2
Hier vind je all info: https://www.manageengine.com/products/active-directory-audit/kb/how-to/how-to-set-logon-hours-in-active-directory.html

==========================================================================================================

### Q3

##### 3.	Toegang tot de gegevens die op de server worden bewaard moet beperkt worden volgens onderstaand schema : 
a.	Homedirectory & profielmap : Alleen de gebruiker zelf
b.	Afdelingsmappen : alleen de leden van de afdeling, directeur en beheerder
c.	Overige : alle medewerkers

### A3
Info kun je hier vinden: https://www.faqforge.com/windows-server-2012-r2/create-home-folder-active-directory-domain-services-windows-server-2012-r2/


==========================================================================================================
# Encryptiebeleid 
==========================================================================================================

### Q1

##### 1.	Alle data op clients moeten voldoende versleuteld zijn.

### A1

Om Bitlocker te installeren op Windows Server 2019: https://abouconde.com/2019/05/20/encrypt-drives-with-bitlocker-on-windows-server-2019/

==========================================================================================================

### Q2
##### 2.	Alle klantgegevens moeten voldoende versleuteld zijn, zowel op interne als externe bronnen als op servers en clients.

### A2
Hier spreken we van SMB (shares) die encrypted moeten zijn: https://docs.microsoft.com/en-us/windows-server/storage/file-server/smb-security#enable-smb-encryption

als je dit enabled dan is er spraken van end-to-end encryption dus bij het verplaatsen van de bestanden, het aanzetten van de encryptie moet dan nog wel gebeuren op de andere servers zie vraag 1 over Bitlocker


==========================================================================================================
# Antivirusbeleid
==========================================================================================================

### Q1
##### 1.	Op elke client en server dient altijd een standaard antivirusoplossing werkzaam en up-to-date te zijn. 

### A1
zie info: 

https://campus.barracuda.com/product/managedworkplace/doc/96765341/setting-up-microsoft-defender-antivirus-policies/

https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/use-group-policy-microsoft-defender-antivirus?view=o365-worldwide

==========================================================================================================

### Q2
##### 2.	Antivirusupdates mogen niet ouder zijn dan twaalf uur.

### A2
Je kunt een Schedule maken die elke 12 uur een update ophaald

informatie hierover:
https://www.urtech.ca/2014/08/solved-how-to-make-windows-defender-to-update-automatically/

Je kunt ook policies aanpassen:
https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/manage-event-based-updates-microsoft-defender-antivirus?view=o365-worldwide

==========================================================================================================

### Q3
##### 3.	Antivirusscans moeten minstens één keer per week op ieder gebruikersapparaat worden uitgevoerd.

### A3
Scan instellen met een schedule:
https://support.microsoft.com/en-us/windows/schedule-a-scan-in-microsoft-defender-antivirus-54b64e9c-880a-c6b6-2416-0eb330ed5d2d

==========================================================================================================

### Q4
##### 4.	Het is alleen voor domain administrators mogelijk om antivirusprogramma’s uit te zetten.

### A4

kun je vinden in de local group policy editor waarschijnlijk

https://www.windows10forums.com/threads/windows-defender-disabled-by-administrator.12890/

==========================================================================================================
