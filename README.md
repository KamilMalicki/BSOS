# BSOS - BootSector Operating System
Program jest prostym monitorem, który działa w trybie rzeczywistym na architekturze x86. Umożliwia użytkownikowi wprowadzenie trzech podstawowych komend do interakcji z pamięcią komputera:

`Wxxxx xx`- Zapisuje wartość pod podany adres pamięci xxxx wartosci heksadecymalne pod xx.

`Rxxxx` - Odczytuje wartość z podanego adresu pamięci xxxx i wyświetla ją na ekranie.

`Xxxxx` - Uruchamia kod znajdujący się pod adresem xxxx.

Program działa w trybie tekstowym i używa standardowych usług BIOS do wyświetlania tekstu i wczytywania danych z klawiatury.

# Sposób użycia
Po uruchomieniu programu użytkownik zostaje zaproszony do wprowadzenia jednej z trzech komend:

Zapis do pamięci (Wxxxx): Należy podać adres w formacie szesnastkowym, do którego zostanie zapisana wartość.

Odczyt z pamięci (Rxxxx): Należy podać adres, z którego zostanie odczytana wartość i wyświetlona na ekranie.

Wykonanie kodu (Xxxxx): Należy podać adres, od którego komputer zacznie wykonywać zapisany kod.

# Przykład działania
Załóżmy, że chcesz zapisać wartość do pamięci, odczytać ją i uruchomić kod. Oto, jak możesz to zrobić:

Przykład wprowadzenia kodu w pamięci.
Załóżmy, że chcesz wprowadzić do pamięci krótki fragment kodu maszynowego i go uruchomić. Oto przykład:

Kod do wprowadzenia: B4 0E B0 30 CD 10 EA A0 AA 00 00 00

- B4 0E: Instrukcja mov ah, 0x0E, która ustawia funkcję BIOS do wyświetlania tekstu.
- B0 30: Instrukcja mov al, 0x30, która ładuje znak 0 (w formacie ASCII).
- CD 10: Wywołanie przerwania BIOSu int 0x10, aby wyświetlić znak.
- EA A0 AA 00 00 00: Skok do adresu 0xAAA0, co może wskazywać na początek jakiegoś kodu.

Jeśli wpiszesz komendy:
```
RAAA0 --> sprawzamy czy na tym adresie coś się znajduje jeśli nie mozemy wpisywac komendy 
WAAA0 B4 --> mov ah,
WAAA1 0E --> 0x0e
WAAA2 B0 --> mov al,
WAAA3 30 --> 48 --> w ascii '0'
WAAA4 CD --> int
WAAA5 10 --> 0x10
WAAA6 EA --> jmp
WAAA7 A0 
WAAA8 AA
WAAA9 00 ---> adress 0x0aaa0
WAAAA 00
WAAAB 00
XAAA0 --> uruchamiamy program skakając do tego segmentu pamięci
```
To komputer wykona kod zapisany pod adresem 0xAAA0 w góre (w którym znajdują się te instrukcje).

Zaleca się zastosowania na końcu programu instrukcje hlt czyli `C3` co powoduje że zatrzyma wykonywanie następnych instrukcji.

Program został napisany na assemblerze 8086 w 512 bajtach ponieważ kod zajmuje tylko pamięć przeznaczoną dla bootsektora od adresu 0x7c00 do 0x7e00 pod żadnym pozorem nie używać tego adresu w celu pisania kodu bo uszkodzimy program rozruchowy.

Dziękuje za przeczytanie informacji o programie oraz informuje że modyfikowanie jest zabronione podlega prawom autorskim
Kamil Malicki
