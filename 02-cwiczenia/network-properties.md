## Ustawianie parametrów sieci

### Zadania

0. Z wykorzystaniem dowolnych systemów operacyjnych na których potrafisz uruchomić interpreter ``python`` oraz oprogramowania virtualbox odwzoruj poniższy schemat sieci:

![alt text][network]

[network]: ./network.png "Logo Title Text 2"

1. na 1 z komputerów zainstaluj i uruchom program ``server.py`` dostępne pod adresem ``https://github.com/jkanclerz/client-server-chat``
2. na 2 z komputerów zainstaluj i uruchom program ``client.py`` dostępne pod adresem ``https://github.com/jkanclerz/client-server-chat``
3. Manipulując konfiguracją sieci na poziomie virtualbox, uruchom serwer czatu, oraz udostępnij go na wybranym porcie oraz adresie tak aby istniała możliwość połączenia przez inne osoby w obrębie pracowni
4. Zainstaluj oprogramowanie serwera HTTP ``nginx`` lub innego, skonfiguruj plik index.html wg instrukcji, sprawdź dostępność strony z wykorzystaniem dowolnego klienta protokołu ``HTTP`` z różnych konfiguracji IP
5. Posługując się programami tj: ``netstat`` lub ``lsof`` sprawdź na jakich portach zostały uruchomione serwery czatu czy HTTP

Wejściowe parametry sieci
-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 10.0.15.4 | |
| MASKA  | /24 (255.255.255.0) | |
|   |  | |
| PC 2  |  | |
| IP - address  | 10.0.15.6 | |
| MASKA  | /24 (255.255.255.0 )| |

Weryfikacja połączenia

Polecenie
``` PC1: ping 192.168.10.11
    PC2: ping 192.168.10.10
```

Efekt
```    spokojnie sobie działa, nie ma straconych pakietów
```

Statyczna konfiguracja parametrów połączenia
Wejściowe parametry sieci
-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 192.168.10.10 | |
| MASKA  | 255.255.255.0 | |
|   |  | |
| PC 2  |  | |
| IP - address  | 192.168.10.11 | |
| MASKA  | 255.255.255.0 | |
| PC 2  |  | |
| IP - address  | 175.15.205.205 | |
| MASKA  | 255.255.255.0 | |

Weryfikacja połączenia

Polecenie
```PC1: ping 175.15.205.205
   PC1: ping 192.168.10.11
   PC2: ping 192.168.10.10
   połączenie client-server-chat z local storage:
   ls-sprawdzamy najawność client-server-chat
   python3 client-server-chat/server.py  -- na PC1
   python3 client-server-chat/client.py  192.168.10.10 5555 -- na PC2, podłączenie do servera port:5555(dowolny)
```

Efekt
    Przy ping 175.15.205.205 nie będzie miało efektu, bo nie mamy połączenia z takim portem w PC1, 
    ostatnie operacje działają bez zarzutu

Nowa statyczna konfiguracja 

-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |
| IP - address  |192.168.10.10  | |
| MASKA         |255.255.255.0  | |
|               |               | |
| PC 2          |               | |
| IP - address  |192.168.11.11  | |
| MASKA         |255.255.255    | |

Weryfikacja połączenia

Polecenie
```
```

Efekt
```
```

### Utrwalenie konfiguracji

Utrwalenie konfiguracji sieci poprzez wpisywanie w /etc/network/interfaces dla danych adapterów adresu oraz maski(address *.*.*.*; netmask 255.255.255.0) dla tego, żeby za każdym właczeniem maszyny nie potrzebowaliśmy stracenia czasu na dodawanie łączących ip adresów do adapteru

### Warto wiedzieć

-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
| Lokalizacja pliku z konfiguracją sieci| | |
| UP -> Wyłączenie interfejsu sieciowego| ip link set eth1 up|eth1 - adapter sieciowy |
| DOWN -> Włączenie interfejsu sieciowego| ip link set eth1 down| |
| Sprawdzenie obecnych parametrów | | |
| lista wszystkich interfejsów |netstat | |
| Które interfejsy jakie porty słuchają |netstat -ltpn | |

