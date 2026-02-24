# Matrioszka
## Wstęp
Dostałem informacje od znajoemgo, że do ich strony na wordpressie (czemu mnie to nie dziwi) został wstrzyknięty kod, który wystawiał captche wymsuzającą na użytkowniku wciśnięcie kombinacji klawiszy WIN+R i WIN+V. WIN+R, czyli uruchowmienie programu uruchom, WIN+V wklejenie kodu. Następnei wykonywało się połaczenie serwera na którym hsotowany był złośliwy plik.
<img width="695" height="239" alt="image" src="https://github.com/user-attachments/assets/507514bd-061f-4e03-86ec-17de035c5e79" />

Następnie pobierany i wykonywany był plik z poniższym zaciemnionym powershellem (fragment).

<img width="1696" height="681" alt="image" src="https://github.com/user-attachments/assets/58b7a2c9-ad07-454d-bc2a-70862d261da6" />

Tak więc przystąpiłem znowu do analizy

##Analzia
Po zdekodowaniu Base64 otrzymano poniższy ciąg, który również był zakodowany w base64

<img width="1523" height="884" alt="image" src="https://github.com/user-attachments/assets/16045f62-8bab-42c1-88ac-0a21ce2a09b3" />

<img width="1701" height="775" alt="image" src="https://github.com/user-attachments/assets/fe466a60-efcd-401d-b2e0-8d5917aebbc5" />

Kod 

<img width="1428" height="79" alt="image" src="https://github.com/user-attachments/assets/53658e24-1f0d-465d-95fb-a193b5418185" />

Sprawdza nazwę komputera (COMPUTERNAME) jeśli zaczyna się od:
WEBSRV + cyfry → „Web server role detected.”
DBSVR + cyfry → „Database server role detected.”
w innym przypadku → „General server role.”

Problem w tym, że ten kod nigdy się nie wykona. Losuje liczbę pomiędzy 1000, a 5000, a ona nigdy nie będzie mneijsza od 0 (-lt 0).

Po zdekodowaniu kolejnej części kodu otrzymujemy ponownie, część z kodem zakodowanym w base64 oraz część, która nigdy się nie wykona.

<img width="1696" height="327" alt="image" src="https://github.com/user-attachments/assets/bf816481-0db2-417b-aa3a-21da67fa0cd2" />

Po ponownym zdekodowaniu otrzymujemy już coś ciekawszego.

<img width="1704" height="453" alt="image" src="https://github.com/user-attachments/assets/ef8accdf-8bd9-4e4f-952f-492f6024dcfa" />

Ponownie część która nigdy się nie wykona

<img width="450" height="80" alt="image" src="https://github.com/user-attachments/assets/88a68f5b-5636-489f-8c04-fc4e819ae80e" />

Oraz ta ciekawsza

<img width="1699" height="85" alt="image" src="https://github.com/user-attachments/assets/6a8c7066-c182-4303-94ee-9560842b22d6" />

- "*" - dowolny znak dowolną ilość razy, bądź jego brak
- "?" - dowolny pojedyńczy znak

Alliasy
- gal - Get-ALias
- gcm - Get-Command
- saps - Start-Process

Po odciemnieniu wyglądał nastepująco

<img width="836" height="80" alt="image" src="https://github.com/user-attachments/assets/c1266641-f9f1-458b-9a0d-a46c928fd84d" />

Kod ten uruchamia powershella, który w trybie cichym, bezokienkowym wykonuje kod ze strony "dock-pointed.softbridge.in.net/glaring-folder-msdn" oraz na końcu utrzyuje wiecznie proces w pętli while.

Przejdźmy zatem w anyrun do strony, do której odwołuje się złośliwy kod i co wykonuje.

<img width="591" height="334" alt="image" src="https://github.com/user-attachments/assets/e361ba53-33fe-4d48-bf7c-19c0cb1892bd" />

AnyRun nic nie wykrył. Spróbujmy zatem przeprowadzić analize w sandbox'ie CrowdStrike. 

<img width="605" height="379" alt="image" src="https://github.com/user-attachments/assets/0d070d83-4477-44fe-9d9d-95cec317793d" />

Przenoszeni zostajemuy na strone z informacjami ze świata - apnews.com. Wayback machine nie znajduje strony w kodzie.

<img width="832" height="488" alt="image" src="https://github.com/user-attachments/assets/51f09e40-0988-4ce6-a57c-2cab5251ddde" />

Aktualnie zdetonowanie próbki w anyrun nie prowadzi do żadnej innej poszlaki. 

TO DO:
- coś wykminić
- analiza index








