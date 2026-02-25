# Matrioszka
## Wstęp
Dostałem informacje od znajoemgo, że do ich strony na wordpressie (czemu mnie to nie dziwi) został wstrzyknięty kod, który wystawiał captche wymsuzającą na użytkowniku wciśnięcie kombinacji klawiszy WIN+R i WIN+V. WIN+R, czyli uruchowmienie programu uruchom, WIN+V wklejenie kodu. Następnei wykonywało się połaczenie serwera na którym hsotowany był złośliwy plik.
<img width="697" height="240" alt="image" src="https://github.com/user-attachments/assets/9fdead63-155a-4d81-9043-bc76e925072b" />

Następnie pobierany i wykonywany był plik z poniższym zaciemnionym powershellem (fragment).

<img width="846" height="339" alt="image" src="https://github.com/user-attachments/assets/813716f3-c686-4d92-a7e3-25e4d2838e83" />

Tak więc przystąpiłem znowu do analizy

##Analzia
Po zdekodowaniu Base64 otrzymano poniższy ciąg, który również był zakodowany w base64

<img width="841" height="485" alt="image" src="https://github.com/user-attachments/assets/5b209cbd-fc02-47e2-87ff-34f3ffa0e37b" />

<img width="838" height="388" alt="image" src="https://github.com/user-attachments/assets/55b7b265-f296-4fdf-8d1f-3dc867cac3ed" />


Kod 

<img width="840" height="48" alt="image" src="https://github.com/user-attachments/assets/b4887257-bf8e-4bf8-b412-d26aeef9614e" />

Sprawdza nazwę komputera (COMPUTERNAME) jeśli zaczyna się od:
WEBSRV + cyfry → „Web server role detected.”
DBSVR + cyfry → „Database server role detected.”
w innym przypadku → „General server role.”

Problem w tym, że ten kod nigdy się nie wykona. Losuje liczbę pomiędzy 1000, a 5000, a ona nigdy nie będzie mneijsza od 0 (-lt 0).

Po zdekodowaniu kolejnej części kodu otrzymujemy ponownie, część z kodem zakodowanym w base64 oraz część, która nigdy się nie wykona.

<<img width="841" height="160" alt="image" src="https://github.com/user-attachments/assets/a2609a48-24ab-4d5d-b102-ea0a860a71b8" />


Po ponownym zdekodowaniu otrzymujemy już coś ciekawszego.

<img width="839" height="225" alt="image" src="https://github.com/user-attachments/assets/91a2891f-9980-4f15-9ee8-a03f7cad1fcc" />

Ponownie część która nigdy się nie wykona

<img width="452" height="81" alt="image" src="https://github.com/user-attachments/assets/8c8b87ce-0c35-4b52-a6bd-0188692da38e" />

Oraz ta ciekawsza

<img width="842" height="49" alt="image" src="https://github.com/user-attachments/assets/97f063c8-7213-4b1d-bda6-d81e6ab1e785" />

- "*" - dowolny znak dowolną ilość razy, bądź jego brak
- "?" - dowolny pojedyńczy znak

Alliasy
- gal - Get-ALias
- gcm - Get-Command
- saps - Start-Process

Po odciemnieniu wyglądał nastepująco

<img width="838" height="82" alt="image" src="https://github.com/user-attachments/assets/f70249e9-ba00-4169-8a13-7490b520db1f" />

Kod ten uruchamia powershella, który w trybie cichym, bezokienkowym wykonuje kod ze strony "dock-pointed.softbridge.in.net/glaring-folder-msdn" oraz na końcu utrzyuje wiecznie proces w pętli while.

Przejdźmy zatem w anyrun do strony, do której odwołuje się złośliwy kod i co wykonuje.

<img width="592" height="334" alt="image" src="https://github.com/user-attachments/assets/012ccf75-5a98-401d-ac4a-1aeeb70c95dd" />

AnyRun nic nie wykrył. Spróbujmy zatem przeprowadzić analize w sandbox'ie CrowdStrike. 

<img width="603" height="377" alt="image" src="https://github.com/user-attachments/assets/1eb965d4-797a-4023-bfe1-959940b01c87" />

Przenoszeni zostajemuy na strone z informacjami ze świata - apnews.com. Wayback machine nie znajduje strony w kodzie.

<img width="835" height="487" alt="image" src="https://github.com/user-attachments/assets/d2a52674-0513-4d0a-a62a-3c49bf23f098" />

Aktualnie zdetonowanie próbki w anyrun nie prowadzi do żadnej innej poszlaki. 

TO DO:
- coś wykminić
- analiza index








