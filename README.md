Dokumentace k praktické zkoušce
Téma: Správa sítě pod Linuxem
Student: Bergmann
Pracoviště: 15
Datum: 28. dubna 2026
1. Úvod a konfigurace sítě
Cílem práce bylo vytvořit heterogenní síťové prostředí v hypervizoru VMware Workstation Pro. Síť byla nastavena na segment 192.168.50.0/24 v režimu NAT s vypnutým DHCP serverem VMware.
Parametry strojů:
• Windows Server 2022: IP 192.168.50.100, role DHCP server.
• Linux 1 (Fedora KDE): IP 192.168.50.111 (rezervace DHCP).
• Linux 2 (Klon): IP 192.168.50.112 (rezervace DHCP).
[ZDE VLOŽ SCREENSHOT 1: Nastavení IP adresy na Windows Serveru]
[ZDE VLOŽ SCREENSHOT 2: Nastavení DHCP rozsahu (Scope) na Windows Serveru]

2. Služba DHCP a rezervace adres
Na Windows Serveru byla nainstalována role DHCP serveru. Byl vytvořen rozsah (scope) od .110 do .120. Pro oba linuxové systémy byly vytvořeny rezervace na základě jejich MAC adres tak, aby vždy obdržely svou pevnou IP adresu.

[ZDE VLOŽ SCREENSHOT 3: Tabulka DHCP rezervací v administraci Windows Serveru]
[ZDE VLOŽ SCREENSHOT 4: Výpis 'ip a' z Linuxu 1 potvrzující získanou adresu .111]
[ZDE VLOŽ SCREENSHOT 5: Výpis 'ip a' z Linuxu 2 potvrzující získanou adresu .112]

3. Vzdálená plocha (RDP)
Na Windows Serveru byla povolena funkce Remote Desktop (Vzdálená plocha). Na straně Linuxu 1 byl nainstalován klient Remmina. Pro úspěšné navázání spojení bylo nutné v nastavení Windows Serveru vypnout vynucování ověřování na úrovni sítě (NLA) a v Remmině nastavit barevnou hloubku na 16bpp (High Color).

[ZDE VLOŽ SCREENSHOT 6: Nastavení Remote Desktopu na Windows Serveru]
[ZDE VLOŽ SCREENSHOT 7: Okno Remminy na Linuxu 1 zobrazující plochu Windows Serveru]

4. Vzdálená správa přes SSH
Na obou linuxových stanicích byla povolena služba sshd. Byla ověřena funkčnost vzdáleného přístupu z terminálu Linuxu 1 na Linux 2.
Zabezpečení: Na hostitelském systému Windows 10 byl vygenerován pár klíčů pomocí ssh-keygen. Veřejný klíč (ED25519) byl přenesen do obou linuxových systémů do souborů authorized_keys. Tím byl zprovozněn bezheslový přístup z hostitelského PC na oba servery.

[ZDE VLOŽ SCREENSHOT 8: Terminál Linuxu 1 přihlášený přes SSH na Linux 2]
[ZDE VLOŽ SCREENSHOT 9: Příkazový řádek Windows 10 přihlášený k Linuxu 1 bez hesla]


5. Webový server Apache
Na Linuxu 2 byl nainstalován balíček httpd. Server byl spuštěn a povolen ve firewallu. V adresáři /var/www/html/ byl vytvořen soubor index.html s informacemi o studentovi a odkazem na stažení této dokumentace.

[ZDE VLOŽ SCREENSHOT 10: Webový prohlížeč na Windows 10 zobrazující stránku z Linuxu 2]

Závěr
Všechny body zadání byly splněny. Systémy komunikují, DHCP přiděluje adresy podle rezervací a vzdálený přístup je nakonfigurován s důrazem na uživatelský komfort (bezheslové SSH) i funkčnost (RDP).
