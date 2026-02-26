Ostatnio otrzyamłem do analizy dwa zakodowane pliki php j.php oraz s.php. Popełniłem przy nich poniższą analizę :) 

# j.php
## Etap pierwszy
Zakodowany ciąg jest to kod w języku php

<img width="945" height="213" alt="image" src="https://github.com/user-attachments/assets/02c0e24c-0fe1-4278-ae5d-17956a061b47" />

Na początku usystematyzujmy kod, aby odpowiednie funkcje były lepiej widoczne.

<img width="945" height="262" alt="image" src="https://github.com/user-attachments/assets/e5b91c23-0fde-41f9-a948-bab3a6f4b58c" />

Zmienne w języku php inicjuje się z wykorzystaniem symbolu $. Pierwsze dwie zmienne, $icyYU oraz $YoKrR służą do przechowania nazw wykorzystywanych później funkcji.

<img width="945" height="115" alt="image" src="https://github.com/user-attachments/assets/dfd658b8-fbe0-40e7-8d3d-ea49c46a60b2" />

Odpowiednio:
•	$icyYU: str_rot13 - poddaje ciąg kodowaniu ROT13
•	$YoKrR: base64_decode - dekoduje ciąg w base64

<img width="945" height="224" alt="image" src="https://github.com/user-attachments/assets/b0463203-1b40-4340-8215-4f57690a4217" />

Zarówno Error_reporting(0), jak i ini_set('log_errors', 0) -odpowiedzialne są za wyłączenie wyświetlania komunikatów o błędach
Funkcja eval(), w której zakodowana jest dalsza część skryptu pozwala na interpretowanie stringa tak, jakby był on poleceniem php. Cały kod znajduje się w klamrach <?php … ?> pozwalający na określenie interpreterowi, że dane miejsce w kodzie ma być kompilowane w języku php.
Po zdekodowano dalsza część skryptu prezentowała się w poniższy sposób

<img width="945" height="297" alt="image" src="https://github.com/user-attachments/assets/4ccc1f35-cdf1-47f0-b1d4-0ebc6e2df453" />

Zarówno początek jak i koniec zdekodowany został poprawnie.

<img width="945" height="305" alt="image" src="https://github.com/user-attachments/assets/d9ca15dd-64e7-4834-93b5-19dd679dc1dd" />

Środkowa część skryptu została dodatkowo zaciemniona z użyciem kompresji gzip. Po ułożeniu otrzymanego ciągu i zamiany niezdekodowanej części na zmienną $ciąg_gzip kod reprezentował się następująco.

<img width="860" height="858" alt="image" src="https://github.com/user-attachments/assets/7a5cebe4-dfe6-4fb1-9fe4-4fcf00abfbfc" />

Głównym elementem kodu był fragment

<img width="945" height="74" alt="image" src="https://github.com/user-attachments/assets/40133662-e068-4524-b3e4-3006addb8ef2" />

•	substr: zwraca tylko pewną wartość stringa określonego według parametrów

<img width="945" height="207" alt="image" src="https://github.com/user-attachments/assets/32281e98-c6d9-4173-b2c1-32d106bba114" />

•	define: definiuje zmienną, która jest case sensitive

<img width="945" height="155" alt="image" src="https://github.com/user-attachments/assets/e3a15acf-2692-4d8e-b9ae-bc8e1e809a5d" />

•	Explode – dzieli string na tablice stringów

<img width="945" height="468" alt="image" src="https://github.com/user-attachments/assets/a448ef41-0d64-44fc-86e9-a794d09dc4e4" />

Zdekodowany ciąg gzip był dzielony na parę stringów, które następnie przypisywane były do odpowiednich indeksów tablicy $GLOBALS.
Kod sprawdzał, czy w interpreterze php istnieje pewna wbudowana funkcja $GLOBALS[][0], jeżeli nie definiował funkcję hex2bin. Funkcja hex2bin wbudowana została natywnie do php od wersji 5.4

<img width="441" height="494" alt="image" src="https://github.com/user-attachments/assets/32b87d33-b9d5-490c-aa7f-3f76a7236967" />

<img width="945" height="23" alt="image" src="https://github.com/user-attachments/assets/52743369-8f65-4a85-89ba-bdb846c283bd" />

Do tablicy $GLOBALS[..] zapisywane są stringi ciągu gzip po usunięciu pierwszych 10 znaków z początku i 8 od końca, które następnie poddane są dekompresji gzip oraz podzielone względem sekwencji podanej jako pierwszy argument funkcji explode.

<img width="945" height="35" alt="image" src="https://github.com/user-attachments/assets/ccfd5765-20e6-484f-9cdf-49aef63e794f" />

W celu wyciągnięcia wartości tablicy $GLOBALS[…] „wstrzyknięto” w base64 do skryptu poniższy kod.

<img width="945" height="424" alt="image" src="https://github.com/user-attachments/assets/7f2a229e-4db1-461a-94ae-281d1acaf34a" />

<img width="945" height="329" alt="image" src="https://github.com/user-attachments/assets/bbe0d925-35f3-420a-80bc-efc798a4ad6f" />

W wyniku otrzymano wartości tablicy.

<img width="945" height="238" alt="image" src="https://github.com/user-attachments/assets/cdd7bbd5-5aac-4a5f-8b17-fac29b904d6e" />

Posiadając wartości zmiennych w tablicy podstawiono je do kodu.

<img width="416" height="561" alt="image" src="https://github.com/user-attachments/assets/708d1199-7e75-4499-98da-c3a7f8f7f8aa" />

Funkcja sprawdza istnienie hex2bin(), jeżeli warunek zwróci 0, sama ją definiuje.

<img width="945" height="115" alt="image" src="https://github.com/user-attachments/assets/3e2161b7-bc7a-4d27-b6b8-b351c3484540" />

Po odpowiednich zmianach otrzymano

<img width="505" height="185" alt="image" src="https://github.com/user-attachments/assets/ce367178-8464-4b23-9089-29a80739dd11" />

Podobnie z poniższą częścią

<img width="945" height="196" alt="image" src="https://github.com/user-attachments/assets/d7963f9d-7bfb-4418-a2bb-97bbcc479a09" />

Funkcja wykonaj_payload importuje zmienne globalne związane z funkcją wytnij_stringa oraz base64_decode. Następnie na podanym payload’zie wykonywane jest dekodowanie base64 oraz dekompresja gzip oraz odczytywany jest od tyłu.
•	strrev: string zapisywany jest od tyłu 

<img width="945" height="178" alt="image" src="https://github.com/user-attachments/assets/b2f8baf4-d974-4781-b552-21b2ea9ede09" />

## Etap drugi

$payload1 prezentował się następująco

<img width="945" height="36" alt="image" src="https://github.com/user-attachments/assets/287ff9df-a05b-46d1-8666-7af86ad8e9c3" />

Ponownie go zdekodowano

<img width="945" height="325" alt="image" src="https://github.com/user-attachments/assets/6a63b7f9-4754-4e43-8ad3-0c17f3114723" />

Poniżej wyciągnięty ciąg

<img width="945" height="451" alt="image" src="https://github.com/user-attachments/assets/4a74d0be-15ac-4d93-a525-06d978e28aa3" />

Po zdekodowaniu

<img width="945" height="436" alt="image" src="https://github.com/user-attachments/assets/3811f02a-046f-47d4-914c-cdd8bd11e86c" />

Kod ten wygląda podobnie do poprzedniego fragmentu, lecz z pewnymi różnicami np. końcówka.

<img width="945" height="399" alt="image" src="https://github.com/user-attachments/assets/9082d6b7-5bba-48cf-8155-cd7eee4b328c" />

W celu zapisania tego ciągu do pliku wykorzystano:

<img width="945" height="320" alt="image" src="https://github.com/user-attachments/assets/fc3aa331-39fe-4c5c-966b-9ea42b166670" />

Po zdekodowaniu

<img width="1002" height="203" alt="image" src="https://github.com/user-attachments/assets/cb078299-43c6-4a0a-84ad-92828ebd0686" />

Zmienne celowo są zaciemnione z wykorzystaniem „.”, która służy w php do składania ciągów stringów w jeden. Żeby utrudnić rozkodowywanie w zmiennej zostało naprzemiennie użyte „0” i „O”.

<img width="945" height="229" alt="image" src="https://github.com/user-attachments/assets/8e61f14a-f434-48dd-a2ef-21b2eeacee1f" />

Ponownie „wstrzyknięto”, który umożliwił wyczytanie wartości tablicy $GLOBALS.

<img width="945" height="351" alt="image" src="https://github.com/user-attachments/assets/f14e398c-1603-4b66-95ba-d39cad5cbf0a" />

Otrzymano

<img width="945" height="198" alt="image" src="https://github.com/user-attachments/assets/843092c8-c082-459d-8e5f-7bb40b157cb8" />

Zdekodowano pierwszy ciąg

<img width="520" height="52" alt="image" src="https://github.com/user-attachments/assets/f13e2692-3e9f-4564-ac72-505ef4c931a5" />

•	urldecode: używany do dekodowania URL zakodowanego przez funkcję encode ().

<img width="945" height="149" alt="image" src="https://github.com/user-attachments/assets/96a3cf27-3ea6-4ed3-af50-cd98bfb0e6e2" />

Z odczytanego ciągu tworzone są poniższe zmienne 
•	$O00O0O
•	$O0OO00
•	$OO0O00
•	$OO0000

<img width="945" height="117" alt="image" src="https://github.com/user-attachments/assets/0b87c8f5-580e-4ed0-a40e-8edf4780fb52" />

Warto zauważyć, że część zmiennych tworzona jest w oparcie o zdekodowany ciąg, a część wykorzystuje zmienne utworzone w poprzednich liniach kodu.
Przykład

<img width="945" height="96" alt="image" src="https://github.com/user-attachments/assets/49db34d3-9271-43fe-91c0-500e62732b07" />
<img width="945" height="96" alt="image" src="https://github.com/user-attachments/assets/dbd1fed9-0ea0-4fab-9db7-b4fe719e8d0e" />

Po zdekodowaniu

<img width="945" height="425" alt="image" src="https://github.com/user-attachments/assets/4e539f7f-12ed-45a6-9824-9746aef6c1ca" />

Po połączeniu z kodem

<img width="550" height="211" alt="image" src="https://github.com/user-attachments/assets/906984c3-bc47-46d3-94c0-3af91d1094ed" />

Zdekodowano ciąg

<img width="945" height="329" alt="image" src="https://github.com/user-attachments/assets/e3244249-5b25-4877-89bb-ef0d17a6cc55" />

<img width="945" height="116" alt="image" src="https://github.com/user-attachments/assets/d9a70c4e-2953-4149-854f-71e4a79f5e16" />

Po ułożeniu i zmianie zmiennych

<img width="945" height="50" alt="image" src="https://github.com/user-attachments/assets/7404bfc6-2df5-4813-9d11-59e732f66c54" />

•	strtr – służy do zastępowania ciągów innymi ciągami

## Etap trzeci

Po zdekodowaniu ciągu

<img width="945" height="288" alt="image" src="https://github.com/user-attachments/assets/784faca9-ee7d-4bba-9001-97f11213950c" />

Kod ułożono

<img width="945" height="881" alt="image" src="https://github.com/user-attachments/assets/d2c947ef-0058-4de2-95ca-511cea20050b" />

Ponownie wstrzyknięto kod w celu poznania wartości macierzy $GLOBALS.

<img width="945" height="246" alt="image" src="https://github.com/user-attachments/assets/27d55bd8-dc1a-45bb-b6e0-d56e8653cb73" />

•	goto - służy do przenoszenia kolejności interpretowanych linii w kodzie do odpowiednich etykiet 
<img width="503" height="566" alt="image" src="https://github.com/user-attachments/assets/b9e383cd-fad0-4c86-8833-2a5c6494ac22" />

Po ułożeniu kodu i rozłożeniu działania etykiet goto

<img width="945" height="368" alt="image" src="https://github.com/user-attachments/assets/55ec6dad-6cba-42b1-a9bc-dd5c9f4b113b" />

Funkcja ta przyjmuje dane w systemie hex, a następnie zamienia je na surowy string binarny.
Przykład
<img width="945" height="406" alt="image" src="https://github.com/user-attachments/assets/983c72c7-f2a1-41d0-97fa-9fed852ba055" />

Zamieniono ją na jej odpowiednik

<img width="945" height="433" alt="image" src="https://github.com/user-attachments/assets/7be8c5fd-4e95-4956-bf15-876ab7cbe41d" />

W wyniku otrzymano

<img width="722" height="59" alt="image" src="https://github.com/user-attachments/assets/988d0637-8fe3-4dc3-9588-618d23c66f9a" />

Po zdekodowaniu ciągu otrzymano

<img width="945" height="369" alt="image" src="https://github.com/user-attachments/assets/8c617d7b-3c19-40f5-b5a9-07a3a34f6cf9" />

## Etap czwarty

Po zdekodowaniu ciągu otrzymano kod przypominający docelowego webshella (poniżej mały fragment)

<img width="945" height="520" alt="image" src="https://github.com/user-attachments/assets/e7f8bd47-760f-484c-94e3-c00ed4766ffe" />

Ponownie w celu wyciągnięcia wartości macierzy $GLOBALS wstrzyknięto odpowiedni kod.

<img width="721" height="827" alt="image" src="https://github.com/user-attachments/assets/625d5373-3ee5-4229-a51e-d14c35abb078" />

Tablica tym razem zawierała 812 elementów.
Po rozkodowaniu przykładowego fragmentu reprezentował się następująco

<img width="945" height="182" alt="image" src="https://github.com/user-attachments/assets/428f032a-ad2d-4d3c-8667-26f73c2e0fbd" />

Do zdekodowania reszty wykorzystano skrypt python. 

<img width="945" height="501" alt="image" src="https://github.com/user-attachments/assets/a4cb8818-aa32-464c-aeb6-ad8fd31edc4a" />

Całość ułożono i rozkodowano 

Webshell po uruchomieniu wyglądał następująco

<img width="945" height="248" alt="image" src="https://github.com/user-attachments/assets/34d9feba-cefe-47c2-99d2-b90463faf234" />

Posiadał funkcję:
•	Sec. Info: pozwala na zdobycie informacji o systemie i uprawnieniach (w tym dostęp do pliku /etc/pass
<img width="698" height="757" alt="image" src="https://github.com/user-attachments/assets/e856c375-a1eb-4649-83ce-490eb1aff8e2" />

•	Files: służy do przeglądania plików
<img width="945" height="186" alt="image" src="https://github.com/user-attachments/assets/6202dacb-db86-4510-9d72-ce62da8bdbc1" />

•	Console: interpreter poleceń systemowych
<img width="945" height="214" alt="image" src="https://github.com/user-attachments/assets/8377e817-f443-4f3a-a7d8-bfd5f9a8d0f4" />

•	Sql: moduł związany z atakimi/obsługą baz SQL
<img width="945" height="136" alt="image" src="https://github.com/user-attachments/assets/c8bb2827-78c1-47ff-a69a-07bb4d9342d4" />

•	Update/Upgrade – ulepszenie do wersji premium oprogramowania (najprawdopodobniej dodatkowo płatne). Brak danych najprawdopodobniej ze względu na brak łączności z internetem maszyny wirtualnej
<img width="945" height="255" alt="image" src="https://github.com/user-attachments/assets/19a6d067-7492-4685-a3d0-057afb766026" />

•	PHP – interpreter php
<img width="945" height="192" alt="image" src="https://github.com/user-attachments/assets/ee3042fe-d2d7-4032-86f4-be4ef4bbdfbb" />

•	String tools: konwersja stringów
<img width="945" height="479" alt="image" src="https://github.com/user-attachments/assets/6377ef12-5f9b-4076-9e00-ff1e4d5a8695" />

•	Bruteforce: ataki siłowe
<img width="909" height="380" alt="image" src="https://github.com/user-attachments/assets/c046bf51-ce12-42a6-b4a6-de2ea44905b4" />

•	Network:  bindowanie portów, obsługa reverse shell’a
<img width="945" height="160" alt="image" src="https://github.com/user-attachments/assets/49dbaa93-ebd2-4070-9a6c-fcb187738350" />

•	Self remove: autodestrukcja
<img width="398" height="139" alt="image" src="https://github.com/user-attachments/assets/a367aa56-3815-4763-a27d-90e4ba7aec70" />

Posiadając wszystkie możliwe do wyciągnięcia informacje rozpoczęto analizę drugiego pliku s.php

# s.php
Podczas próby jego uruchomienia, okazało się, że zawartość jest chroniona hasłem.

<img width="833" height="280" alt="image" src="https://github.com/user-attachments/assets/d1cef4be-9ead-4f9b-b148-be4bd1bb0001" />

Kod s.php wyglądał następująco

<img width="945" height="195" alt="image" src="https://github.com/user-attachments/assets/55fd9ac2-5d73-4c76-8d59-effd489d52e3" />

Kod ułożono i poddano dekodowaniu base64

<img width="945" height="519" alt="image" src="https://github.com/user-attachments/assets/158e6dcb-92a5-42a8-8fde-e4816ce14367" />

## Etap pierwszy

Zaczęto od pierwszej części kodu

<img width="945" height="151" alt="image" src="https://github.com/user-attachments/assets/2cbb6771-b50a-4253-afe8-cd2f6a18fa9b" />

•	hex2bin – konwertuje hex na ASCI (wynik w stringu)
•	int – zamienia stringa na int

<img width="945" height="283" alt="image" src="https://github.com/user-attachments/assets/709da43d-d9f6-4a99-917d-d524a903d9db" />

Zatem po zebraniu kod wyglądał następująco

<img width="573" height="228" alt="image" src="https://github.com/user-attachments/assets/041032cc-0497-4b75-a398-61460f9aba39" />

Funkcja najpierw usuwa 908 pierwszych znaków z payload’u, a następnie usuwa 573 znaków od końca.

Następnie rozkodowano poniższą funkcję

<img width="945" height="182" alt="image" src="https://github.com/user-attachments/assets/98ee9b51-8119-44ac-bc5f-cd989798b73c" />

Jest to funkcja, która jako argument przyjmuje pewnego stringa, następnie jest on poddawany funkcji wytnij_stringa, po czym decodowany z base64 i na końcu poddawany jest dekompresji gzip. Przyjęto zatem.

<img width="945" height="159" alt="image" src="https://github.com/user-attachments/assets/259d131d-d67f-4208-802b-3a5b016a7b51" />

Z ciągu usunięto zbędne wywołania funkcji eval.

<img width="945" height="154" alt="image" src="https://github.com/user-attachments/assets/31b4d87e-114e-497a-b410-183e56c925d9" />

Po zdekodowaniu

<img width="945" height="409" alt="image" src="https://github.com/user-attachments/assets/781543ea-1c49-49a7-a335-7ef5f1945769" />

## Etap drugi

Po zapisaniu, kod reprezentował się następująco

<img width="945" height="502" alt="image" src="https://github.com/user-attachments/assets/e12cf344-92ba-4f44-87c8-0487c80f4674" />

Całość kodu do zaciemnienia i utrudnienia analizy wykorzystuje wiele etykiet goto, które mogą sprawnie ukrywać zarówno pętle logiczne jak i elementy typu switch. 
Poniżej część kodu przed usunięciem etykiet.

<img width="945" height="339" alt="image" src="https://github.com/user-attachments/assets/ea82082f-6fbe-43ff-ab2e-8a31595b1511" />

Ten sam kod po usunięciu etykiet i zastąpieniu jej funkcjami im odpowiadającymi.

<img width="689" height="864" alt="image" src="https://github.com/user-attachments/assets/2feb51ba-b1c7-43c1-a960-3868d2fc51aa" />

Następnie w celu zdobycia hasła do webshella sprawdzono jak w kodzie źródłowym na stronie wygląda odpytanie hasła.

<img width="945" height="219" alt="image" src="https://github.com/user-attachments/assets/bf100153-9f7d-447b-a1a1-ebce9e91fab6" />

Znaleziono podobne miejsce w kodzie.

<img width="945" height="36" alt="image" src="https://github.com/user-attachments/assets/5a38efb8-6afe-46d3-aa38-332a5d1dbf65" />


Po analizie metody POST odnaleziono poniższą instrukcję warunkową przyrównującą wartość POST[‘pass’] do zmiennej.

<img width="945" height="167" alt="image" src="https://github.com/user-attachments/assets/9d3f5ba5-b8ec-4143-a7a6-b7ceb1841463" />

Wartość zmiennej zapisana była zwykłym tekstem w kodzie bez szyfrowania ani wykorzystania hash z solą, także można było je od razu odczytać.

<img width="176" height="51" alt="image" src="https://github.com/user-attachments/assets/7adc10f6-cf5c-408e-9586-faf2d97e96c6" />

Celowo uciąłem część związaną z hasłem. Nie będę aż tak ułątwiał komuś życia :)

Po wpisaniu hasła uzyskano dostęp do webshella w wersji premium.

<img width="945" height="219" alt="image" src="https://github.com/user-attachments/assets/2445893c-08f6-472e-a9ed-177350253a1d" />

Dodatkowe funkcje:
•	Infect – funkcja, do infekcji serwera (w celu jej pełnego zrozumienia należałoby całkowicie odekodować plik s.php)
<img width="945" height="168" alt="image" src="https://github.com/user-attachments/assets/581bb77f-60c0-41a7-8e0a-148a91f40b51" />
•	Safemode: służy do bypass’owania funkcji safemode
<img width="945" height="208" alt="image" src="https://github.com/user-attachments/assets/3d5ca8da-c64c-4365-bb62-44585a3a0c56" />
Dodatkowo w porównaniu z sekcjami z poprzedniego webshella posiada rozbudowane informacje
•	Sec.info
<img width="945" height="351" alt="image" src="https://github.com/user-attachments/assets/86078a5c-9b40-4c82-a8cc-14560e2aa325" />
•	Sql (więcej opcji jest writable)
<img width="945" height="163" alt="image" src="https://github.com/user-attachments/assets/1bd2c5f8-b20d-41de-a2a5-3aa75ed191ee" />


