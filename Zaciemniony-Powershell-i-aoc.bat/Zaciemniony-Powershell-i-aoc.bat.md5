# Zaciemniony-Powershell-i-aoc.bat

Ostatnio bylem w pracy świadkiem bardzo ciekawego incydentu. Loader został zablokowany więc mogłem, z 50% spokojem, wziąć się od razu do roboty związanej z inżynierią wsteczną poniższego kodu.

<img width="975" height="467" alt="image" src="https://github.com/user-attachments/assets/f2c13396-6b2a-4d3f-b8c6-a91a5214d915" />

Od razu przykuwa uwagę fakt, że mamy do czynienia z kodowaniem Base64. Warto jednak zwrócić szczególną uwagę na fragment końcowy: Replace('oGEbHOmZxiVk',''). Instrukcja ta nakazuje, aby z danego ciągu znaków usunąć wszystkie wystąpienia sekwencji "oGEbHOmZxiVk", czyli innymi słowy – całkowicie ją wyeliminować z tekstu.

<img width="1535" height="859" alt="image" src="https://github.com/user-attachments/assets/ceed44e9-2957-4bcc-8d36-c692c5f3c09c" />

Loader podzielony został na dwie główne sekcje
- sekcja c
- sekcja d

## Sekcja c

Informacje zawarte w każdej z sekcji zostały zakodowane przy użyciu Base64, a następnie skompresowane za pomocą Gzip (dla ilustracji pokazano to na przykładzie sekcji C).

<img width="1527" height="574" alt="image" src="https://github.com/user-attachments/assets/7838c5e3-9a0e-487e-8e82-317ce1146d44" />

Po odpowiednim zmodyfikowaniu sekcja c prezentowała się następująco

<img width="742" height="585" alt="image" src="https://github.com/user-attachments/assets/5e4f0dfe-656f-4e02-8ff2-cc3b4ae314c5" />

Kod przypisuje zmiennej $banana ścieżkę do pliku aoc.bat, który powinien znajdować się w katalogu użytkownika. Następnie weryfikowana jest jego obecność, po czym z pliku odczytywane są te linie, które rozpoczynają się od prefiksów od ::1 do ::5. Z każdej z nich usuwane są cztery pierwsze znaki, a uzyskane w ten sposób fragmenty zostają połączone w jedną całość.

W dalszym etapie z powstałego ciągu eliminowane są sekwencje „surfersparadisemiamibeach” oraz „eRc” (których nie było), co skutkuje utworzeniem właściwego payloadu. Ten zaś jest następnie wykonywany bezpośrednio w pamięci.

## Sekcja D

Zmienne $p1 oraz $p2 tworzą zmienną $d, która odwołuje się do zmiennej $i.  

<img width="1529" height="648" alt="image" src="https://github.com/user-attachments/assets/62419075-f17c-4f1b-95ea-4b8a8e924b43" />

Kod w zmiennej $i po zdekodowaniu wygląda następująco

<img width="1534" height="741" alt="image" src="https://github.com/user-attachments/assets/61c4a35e-c83a-4e63-814a-903432e7d930" />

Łącząc powyższe informacje, zastępując nazwy funkcji bardziej adekwatnymi oraz eliminując zbędne konstrukcje logiczne w rodzaju „1 = 1”, uzyskano poniższą, uporządkowaną wersję kodu.

<img width="1522" height="835" alt="image" src="https://github.com/user-attachments/assets/e0fb3d36-d493-4a9f-8ecb-a256ae504e76" />

Mamy w nim takie elementy jak:
- funkcja deszyfrująca aes
- funkcja dekompresji
- punkcja wykonywania w pamięci

Dodatkowo w tym przypadku kod również odwołuje się do pliku aoc.bat, przy czym wyodrębniany jest ciąg rozpoczynający się od :: , typowego komentarza w plikach .bat. Następnie ciąg ten jest dzielony na dwie części przy użyciu znaku \.

Następnie payloady te po deszyfracji i dekompresji wykonywane są w pamięci.

## aot.bat

Przejdźmy zatem do pliku aoc.bat. Po wstępnych zmianach wyglądał on mniej więcej w poniższy sposób

<img width="1674" height="745" alt="image" src="https://github.com/user-attachments/assets/6141bfa2-1d79-4db1-9e10-6a2e80dcd724" />

Zmienne w środowisku CMD oznaczane są za pomocą notacji %...%. Istotne jest przy tym, że w przypadku odwołania do zmiennej, która nie została zdefiniowana, nie dochodzi do żadnej modyfikacji polecenia ani zmiany jego logiki — odwołanie pozostaje po prostu puste. W konsekwencji wyrażenie s%nbTvA%et "IWKSA=d" w rzeczywistości odpowiada zapisowi set "IWKSA=d".

Mając to na uwadze, początkowy fragment kodu został oczyszczony z nieistotnych, losowych zmiennych, a pozostałe zostały ujednolicone i zastąpione ich rzeczywistymi odpowiednikami, co pozwoliło na uzyskanie bardziej przejrzystej i logicznie spójnej formy.

<img width="1429" height="236" alt="image" src="https://github.com/user-attachments/assets/c0515658-a83d-426a-adef-f3454a3e27db" />

Przeglądając kod znaleziono również komentarze, które dla tych co czytali sekcje c, powinny wyglądać znajomo.

<img width="1687" height="157" alt="image" src="https://github.com/user-attachments/assets/3b2b7ccb-77f2-483e-af84-85b2b5785be0" />

Wynik dekodowania jest na tyle obszerny, że w pliku 1.txt umieszczono jedynie początkowy fragment kodu. Aby zobaczyć jego pełną, pierwotną postać przed zastosowaniem dalszych modyfikacji, warto samodzielnie go zdekodować (Base64 → UTF16-LE), pamiętając przy tym o wcześniejszym usunięciu wskazanych ciągów znaków :).

Po usunięciu czterech pierwszych znaków w każdej linii, eliminacji sekwencji opisanych w sekcji C, dekodowaniu ciągu i podstawieniu zmiennych, przystąpiono do usuwania zbędnych elementów kodu. Ze względu na zastosowanie licznych mechanizmów zaciemniania, omówimy je szczegółowo, krok po kroku.

### operator łańcuchowy
  
<img width="1325" height="26" alt="image" src="https://github.com/user-attachments/assets/e8852659-0e46-481b-8358-5de3c3d1ae57" />

W tym fragmencie {0} i {1} to symbole pozycyjne używane przez operator formatowania łańcuchów w PowerShellu (-f). Czyli końcowy ciąg, będzie wyglądał następująco

<img width="1162" height="27" alt="image" src="https://github.com/user-attachments/assets/e0c233dd-6156-4f0b-9a11-cf3975230350" />

Jest to oczywista próba zasymulowania awarii Amsi poprzez ustawienie pola 'amsiInitFailed' na true, przez co dalsza część skryptu nie podlegałaby skanowaniu.

### ciąg ze zmiennych
  
<img width="565" height="90" alt="image" src="https://github.com/user-attachments/assets/bf3d34b7-ec8f-4c6a-9a05-c396e0ce4a7d" />

Stosowana wcześniej juz metoda, ale tutaj jest najbardziej widoczna. Sygnatura, która mogłoby wywołąć detekcje jest dzielona na parę elementów i rozpisywana do zmiennych.

### końcowe komendy podzielone były na składające się na nią zmienne

<img width="1570" height="106" alt="image" src="https://github.com/user-attachments/assets/2941a5bf-70f9-463e-92e8-16df58b6d088" />

Po zmianach 

<img width="1676" height="35" alt="image" src="https://github.com/user-attachments/assets/e2add027-0b22-44df-a497-f1d0913a977a" />

### zmienne zazębiające się

<img width="1563" height="37" alt="image" src="https://github.com/user-attachments/assets/2634cd85-d9ae-4742-b55e-fc86e177487b" />

W opisanej sytuacji należy zachować ostrożność przy zamianie nazw zmiennych. Jeśli najpierw zmienimy $SetLastError, wszystkie odwołania do $SetLastErrorCustomAttribute ulegną naruszeniu, ponieważ nazwa pierwszej zmiennej jest zawarta w nazwie drugiej. Poprawna kolejność polega na tym, aby najpierw zająć się zmienną $SetLastErrorCustomAttribute, a dopiero potem wprowadzać zmiany w $SetLastError, uzupełniając przy tym wszystkie wcześniejsze odwołania.

## Anazlia kodu (pomoc chatu)
### sekcja pierwsza

<img width="1686" height="313" alt="image" src="https://github.com/user-attachments/assets/14976284-9477-4f86-9189-e7250467f1f4" />

- Manipulacja AMSI
To jest refleksja .NET wykorzystywana do ustawienia na true prywatnego, statycznego pola amsiInitFailed w klasie AmsiUtils. W praktyce oznacza to symulowanie awarii AMSI, czyli mechanizmu analizującego skrypty PowerShell pod kątem złośliwych treści.

- Funkcja isReadable
Ta funkcja ocenia, czy zadany obszar pamięci spełnia kryteria „czytelności” na podstawie flag ochrony (PAGE_READONLY, PAGE_READWRITE, itp.) i stanu (np. MEM_COMMIT).

- Dynamiczne tworzenie struktury MEMORY_INFO_BASIC
Cały blok tworzy dynamiczną strukturę .NET odzwierciedlającą layout pola: BaseAddress, AllocationBase, AllocationProtect, RegionSize, State, Protect, Type

To odpowiada strukturze MEMORY_BASIC_INFORMATION znanej z WinAPI (VirtualQuery). Ta struktura pozwala np. iterować po segmentach pamięci procesu.

### sekcaj druga

<img width="1641" height="266" alt="image" src="https://github.com/user-attachments/assets/178270c5-6930-4dad-aeed-9cb8e085881c" />

- Dynamiczne tworzenie struktury WinAPI SYSTEM_INFO
Definiuje nową strukturę (ValueType) w czasie wykonywania. To odpowiednik struktury SYSTEM_INFO z Windows API, której używa m.in. funkcja GetSystemInfo. W oryginalnym WinAPI SYSTEM_INFO zawiera dane o środowisku systemowym: architektura procesora, liczba procesorów, rozmiar strony pamięci, minimalny/maksymalny adres aplikacji, maska aktywnych procesorów, typ procesora, poziom i rewizja procesora, granularność alokacji.

- Przygotowanie typu Win32.Kernel32
To tworzenie pustej klasy Kernel32, która prawdopodobnie później dostanie: deklaracje funkcji P/Invoke (np. GetSystemInfo, VirtualQuery, ReadProcessMemory, itp.) lub wrappery nad WinAPI.
  
### sekcja 3

<img width="1687" height="691" alt="image" src="https://github.com/user-attachments/assets/5e2b77ac-e346-42bf-8286-ae6f9af87a69" />

- VirtualProtect (kernel32.dll)
Pozwala zmieniać ochronę pamięci (np. z PAGE_READONLY na PAGE_EXECUTE_READWRITE).

- GetCurrentProcess (kernel32.dll)
Zwraca uchwyt do bieżącego procesu. Potrzebne jako „handle” dla innych wywoła

- VirtualQuery (kernel32.dll)
Zwraca informacje o danym regionie pamięci: adres bazowy, rozmiar, typ, uprawnienia (PAGE_xxx), stan (MEM_COMMIT, MEM_FREE...).

- GetSystemInfo (kernel32.dll)
Wypełnia strukturę SYSTEM_INFO, którą wcześniej zbudowano dynamicznie.

- GetMappedFileName (psapi.dll)
Zwraca ścieżkę pliku, który został zmapowany w określonym adresie pamięci.

- ReadProcessMemory (kernel32.dll)
Czyta bajty z pamięci danego procesu.

- WriteProcessMemory (kernel32.dll)
Zapis do pamięci procesu.

- GetProcAddress (kernel32.dll)
Zwraca wskaźnik do funkcji eksportowanej przez określony moduł (DLL).

- GetModuleHandle (kernel32.dll)
Zwraca uchwyt do załadowanego modułu (np. „kernel32.dll”, „ntdll.dll”) bez zwiększania licznika referencji.

## sekcja 4

<img width="1318" height="489" alt="image" src="https://github.com/user-attachments/assets/3c6ee6b2-7fb3-4168-b313-09e91d8681a2" />

- Wymuszenie “FullLanguageMode” i ExecutionPolicy Bypass
To próba: przełączenia PowerShella z trybu ograniczonego na pełny (FullLanguage), ustawienia polityki wykonania na „Bypass”.

- Sprawdzanie i modyfikacja funkcji EtwEventWrite w ntdll.dll
EtwEventWrite to funkcja odpowiedzialna za logowanie zdarzeń do ETW (Event Tracing for Windows). Kod zmienia atrybuty pamięci tej funkcji na wykonywalne/zapisywalne (VirtualProtect → PAGE_EXECUTE_READWRITE), wkleja 1 bajt (0xC3) na x64 albo C2 14 00 na x86.

0xC3 = instrukcja RET, czyli natychmiastowy powrót z funkcji.

Efekt: funkcja przestaje działać. W praktyce uniemożliwia to generowanie zdarzeń ETW przez ten proces.

- Manipulacja AMSI w pamięci procesu
To ustawienie wewnętrznych statycznych pól AMSI na wartości „niezainicjalizowane”.

- Modyfikacja rejestru — usunięcie providerów AMSI
To usuwa podklucze rejestru, w których zarejestrowane są zaufane dostawcy AMSI (np. antywirusy, moduły skanujące).

## sekcja 5

<img width="1400" height="505" alt="image" src="https://github.com/user-attachments/assets/76cc19dc-b064-44c9-b824-a80c7b36e6da" />

- Pobranie informacji systemowych
Ta funkcja wypełnia strukturę SYSTEM_INFO

- Pętla po przestrzeni adresowej
To jest konstrukcja mająca przemieszczać się adres po adresie aż do maksymalnego adresu aplikacji.

- VirtualQuery dla aktualnego adresu
To zwraca szczegóły regionu pamięci

- Filtrowanie: IsReadable + rozmiar > 0x1000
Filtruje to małe lub nieużyteczne fragmenty.

- Próba ustalenia nazwy pliku, z którego pochodzi mapowanie
Jeżeli region pochodzi z pliku (DLL, EXE, mapowany zasób), zwraca jego ścieżkę.

- Szukanie „clr.dll”
Kod szuka obszarów pamięci należących do .NET Common Language Runtime.
CLR zawiera: tablice wskaźników, JIT-owane metody, natywne struktury środowiska .NET, pewne punkty zaczepienia dla hooków lub manipulacji.

## sekcja 6

<img width="1685" height="681" alt="image" src="https://github.com/user-attachments/assets/085551ec-d603-4d6b-b0ba-73c70e8c888d" />

- Przygotowanie zmiennych
Potrzebne dla WinAPI ReadProcessMemory i WriteProcessMemory

- Pętla
Iteracja przez regiony pamięci -> wkanowanie regionu porcjami po 1 MB -> warunek: czy ReadProcessMemory zwrócił coś -> co ma sensowny rozmiar -> Porównywanie bajtów -> gdy znaleziono ciąg — patchowanie -> nadpisanie

### Opis ogólny (też chat pomagał)

Przebieg
1. Próba ustawienia pełnego trybu językowego i polityki (FullLanguage + Bypass).
2. Próba wyłączenia AMSI na poziomie pola amsiInitFailed (wcześniejszy fragment) oraz ustawienie amsiSession/amsiContext na null/zero.
3. Dynamiczne zbudowanie struktur i P/Invoke, aby mieć dostęp do WinAPI z poziomu czystego PowerShella.
4. Sprawdzenie i patchowanie ETW: jeżeli EtwEventWrite istnieje, zastąpienie jej krótką instrukcją powodującą natychmiastowy return, co ma zablokować event tracing.
5. (Opcjonalnie, jeśli dostępny) usunięcie rejestrowanych providerów AMSI w rejestrze.
6. Pobranie systemowych informacji o pamięci i iteracja po przestrzeni adresowej.
7. Dla każdego regionu: VirtualQuery → IsReadable → GetMappedFileName → filtr na clr.dll.
8. Dla regionów CLR: odczyt porcjami → poszukiwanie "AmsiScanBuffer" → jeśli znaleziono: VirtualProtect → WriteProcessMemory (nadpisanie literalów) → przywrócenie ochrony → zakończenie.

Efekt końcowy:
- AMSI w tym procesie: mechanizmy skanujące PowerShella zostaną osłabione lub unieruchomione.
- ETW: proces przestaje emitować pewne zdarzenia przez EtwEventWrite .
- Rejestr AMSI: jeśli usunięcie kluczy powiedzie się, systemowa konfiguracja providerów AMSI może zostać zmodyfikowana.
- Zasoby CLR: literal "AmsiScanBuffer" w obszarach pamięci CLR zostanie nadpisany.

## Próba deszyfracji AES

Następnie przystąpiono do próby odszyfrowania ciągu znaków odpowiadającego za sekcję D. Zgodnie z logiką zaciemnionego skryptu PowerShell należy: odnaleźć ciąg rozpoczynający się od :: , usunąć z niego pierwsze trzy znaki, podzielić go na dwie części, a każdą z nich poddać konwersji z Base64, następnie deszyfrowaniu przy użyciu AES i dekompresji Gzip.

Na początku należało ponownie wrócić do pliku aoc.bat i odnaleźć odpowiedni ciąg. 

<img width="1675" height="14" alt="image" src="https://github.com/user-attachments/assets/9fc30ccf-686a-4997-9c3a-29a0c4fe972f" />

Na szczęście w funkcji szyfrującej użyto stałego wektora oraz klucza, co umożliwiło zdeszyfrowanie kodu.

<img width="708" height="169" alt="image" src="https://github.com/user-attachments/assets/1c51de7a-9401-4d25-b125-22ace7bb427c" />

Po zdekodowaniu zmiennej $payload1 okazało się, że jej zawartość stanowi plik binarny. Analogiczną operację przeprowadzono dla $payload2, zapisując uzyskane dane odpowiednio do plików $payload1.exe oraz $payload2.exe. Należy jednak podkreślić, że w oryginalnym skrypcie oba ładunki były wykonywane wyłącznie w pamięci operacyjnej, bez ich fizycznego zapisu na dysku komputera ofiary.

<img width="2020" height="1074" alt="image" src="https://github.com/user-attachments/assets/ed36d051-ce57-4806-a214-16e41207c8de" />

## paylaod1.exe

Plik zgodnie z założeniami okazał się plikiem wykonywalnym.

<img width="837" height="60" alt="image" src="https://github.com/user-attachments/assets/0b47ee70-03d9-44e8-ac82-2357dbc23e0a" />

Za pomocą komendy strings znaleziono manifest odpowiedzialny za sposób uruchamiania procesu w kontekście UAC.

<img width="594" height="185" alt="image" src="https://github.com/user-attachments/assets/fce224e9-eb60-424e-aee0-d80ad42c5762" />

Oznacza to:
- proces uruchamia się z tymi samymi uprawnieniami co rodzic
- NIE próbuje eskalacji do administratora
- NIE wyświetla prompta UAC

### Analiza sandbox

#### Virus Total

<img width="1310" height="544" alt="image" src="https://github.com/user-attachments/assets/9f5fa976-0ce0-4502-9c5c-3fae5df49c91" />

Analzia w VirusTotal wskazała na aplikację typu Trojan.

#### AnyRun

Ku mojemy jednoczesnemu zasmuceniu (spędzę nad tym plikiem kolejne 10 h) i podekscytowaniu (szykuje się coś ciekawszego) AnyRun nie wykazał żadnego zagrożenia.

<img width="644" height="307" alt="image" src="https://github.com/user-attachments/assets/9ca754b2-3796-4aa9-a44d-21ec78a3999d" />

Podsumowywując na tym etapie wiemy, że jest złośliwy.... nic nowego.

### Analiza statyczna

#### Detect It Easy (do dokończenia)

<img width="1214" height="206" alt="image" src="https://github.com/user-attachments/assets/5a4e72d0-bd57-430a-95a7-4e894e90e385" />

### Dekompilacja (do zrobienia)

Na tym etapie pozostawię temat nierozwinięty, ponieważ mam świadomość, że gdy tylko się za niego zabiorę, najpewniej pochłonie on nie tylko najbliższe dni, ale wręcz dobre dwa lata mojego życia. Dla porządku, aby nic istotnego nie umknęło: konieczna będzie analiza rejestru na maszynie z systemem Windows REM. Niewykluczone również, że mechanizm ten wymaga uruchomienia z określonymi parametrami — to także pozostaje do zweryfikowania.

## payload2.exe

Plik ten również okazał się być plikiem wykonywalnym.

<img width="813" height="65" alt="image" src="https://github.com/user-attachments/assets/73f58762-6ff8-4f11-b9b0-2378cd7b2db4" />

Manifest wyglądał identycznie jak w przypadku payload1.exe

### Analiza Sandbox

#### VirusTotal

W tym wypadku sandbox jednoznacznie stwierdził, że oprogramowanie jest trojanem.

<img width="1313" height="841" alt="image" src="https://github.com/user-attachments/assets/8af5d14c-45de-410c-9ba5-2192e072b0f9" />

#### AnyRun

W tym miejscu dysponujemy już kompletnym zestawem informacji.

<img width="639" height="436" alt="image" src="https://github.com/user-attachments/assets/077751fe-c439-43a3-8bf6-3afcc5a6b6ce" />


AnyRun jednoznacznie stwierdził, że jest to XWORM, oprogramowanie typu RAT (Remote Acess Trojan) - https://any.run/malware-trends/xworm/


<img width="1849" height="452" alt="image" src="https://github.com/user-attachments/assets/bb83dcd4-9d1b-4dd7-91ad-ed567d2814a7" />

##### IOC
Plik
- dodawał sam siebie do autostartu
- wyłączał Windows Event Logging
- łączył się z adresem 103.83.86.27 (najprawdopodbniej za pomocą telegrama)
<img width="749" height="362" alt="image" src="https://github.com/user-attachments/assets/fa8cfb01-e51a-42ce-a92a-c2915a836702" />

#### tria.ge

Triage również potwierdził złośliwość pliku

<img width="1534" height="483" alt="image" src="https://github.com/user-attachments/assets/981548ae-0739-4337-9690-1879d89ebb79" />

<img width="762" height="837" alt="image" src="https://github.com/user-attachments/assets/af825cee-2a2b-402d-b8a0-e815429f9c96" />

#### IOC
Plik
- tworzył pliku C:\Users\Admin\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\XWormClient.lnk
- otwierał i modyfikował C:\Users\Admin\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\XWormClient.lnk
<img width="1899" height="208" alt="image" src="https://github.com/user-attachments/assets/6123cb23-604f-4470-a12a-c282034f1636" />

https://tria.ge/251125-raxh9awran/pdf-report.html?c (analiza dla chętnych)

## Powrót do aoc.bat

Skoro pliki mamy przeanalizowane wróćmy do aoc.bat, gdyż został ostatni element do przeanalizowania

<img width="815" height="19" alt="image" src="https://github.com/user-attachments/assets/50d58867-b26b-4a6a-93a4-16bff255a4fd" />

W tym celu ponownie należy pozbyć się zbędnych zmiennych. Na szczęście w każdej osobnej lini znajduje się ta sama zmienna zaciemniająca. 

<img width="1675" height="517" alt="image" src="https://github.com/user-attachments/assets/0d001d10-dddb-4502-abbe-d7a0eff8a298" />

Aby go odkodować należy zmienić wszystkie zmienne na odpowiadające im wartości (kawałek poniżej)

<img width="474" height="601" alt="image" src="https://github.com/user-attachments/assets/923fe744-6b64-4bc6-aa07-31c8319a07eb" />

W wyniku otrzymano 

<img width="1882" height="657" alt="image" src="https://github.com/user-attachments/assets/59274d61-b5b8-44f8-b27b-08b036dd27cd" />

Czyli powershell, który był powodem początkowej detekcji.

Na samym końcu znaleziono jeszcze poniższe ciągi.

<img width="381" height="66" alt="image" src="https://github.com/user-attachments/assets/f35bb1a0-c7c6-4967-9853-18c40abc76b0" />

Po zdekodowaniu można je zapisać w formie "timeout /t 1 /nobreak >nul", czyli zatrzymanie działania skryptu na 1 sekundę, nie pozwala przerwać go klawiszem oraz nie pokazuje żadnego komunikatu.

