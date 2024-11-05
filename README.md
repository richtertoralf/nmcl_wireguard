# nmcli_wireguard
**schnelle Variante zur Einrichtung einer Wireguard Schnittstelle mit nmcli (NetworkManager)**

>Immer mehr Linux Disributionen nutzen NetworkManager zur Verwaltung der Netzwerkschnittstellen.
>Traditionell waren für Wireguard `openresolve` oder `resolveconf` zur Namensauflösung vorgesehen. Unter Ubuntu 24.04 wird aber `sytemd-resolved` dafür verwendet, was bei Verwendung des Wireguard-Tools wg-quick zu Konflikten führen kann.
>Anstatt wg-quick zu verwenden, kann die Wireguard-Schnittstelle auch sehr einfach mit dem Networkmanager-Tool `nmcli` hinzugegfügt werden.
>Die folgende Variante funktioniert auch sehr gut mit dem RasperryPi OS bookworm.

## Installation
```
sudo apt install wireguard
```
Danach lege ich eine fertige Wireguard-Konfiguration `wclient112.conf` ins Verzeichnis `/etc/wireguard`
## Wireguard-Konfigurationsdatei (Beispiel)
```
[Interface]
PrivateKey = xxxxxxxxxxxx=
Address =172.16.100.112/32
DNS = 1.1.1.1

[Peer]
PublicKey = yyyyyyyyyyyy=
Endpoint = xxx.xxx.xxx.xxx:51820
AllowedIPs = 172.16.100.0/24
PersistentKeepalive = 25

# created 2024-11-05 22:58:31.64813
```
## Wireguard-Konfiguration importieren
```
nmcli connection import type wireguard file /etc/wireguard/wclient112.conf
```
## Wireguard-Schnittstelle aktivieren
```
nmcli connection up wclient112
```
## Schnittstelle anzeigen lassen
Die vom NetworkManager verwalteten Verbindungen werden automatisch unter `/etc/NetworkManager/system-connections/` abgelegt.
Dort finden wir jetzt auch unsere Beispielverbindung `wclient112.nmconnection`.
