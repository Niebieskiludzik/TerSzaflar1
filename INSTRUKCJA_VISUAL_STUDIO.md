# 🎮 Jak skompilować grę do pliku .exe w Visual Studio 2022

Ten przewodnik wyjaśnia krok po kroku, jak uzyskać działający plik `dungeon_game.exe` na Twoim komputerze.

---

## KROK 1: Wymagania wstępne w Visual Studio 2022

Do skompilowania kodu C++ potrzebujesz darmowego **Visual Studio 2022 Community** (lub Professional/Enterprise):
1. Otwórz program **Visual Studio Installer** na komputerze.
2. Przy swojej wersji Visual Studio 2022 kliknij **Modyfikuj** (*Modify*).
3. Na liście "Pakiety robocze" upewnij się, że zaznaczona jest opcja:
   - ✅ **Programowanie aplikacji klasycznych w języku C++** (*Desktop development with C++*)
   *(Pakiet ten zawiera kompilator MSVC oraz wbudowane narzędzia CMake dla systemu Windows).*
4. Jeśli nie była zaznaczona, zaznacz ją i kliknij "Zainstaluj podczas pobierania".

---

## KROK 2: Otwarcie projektu w Visual Studio

Nie musisz tworzyć ręcznie żadnych solucji `.sln` ani dodawać plików pojedynczo! Visual Studio ma wbudowaną natywną obsługę projektów CMake.

1. Pobierz archiwum projektu klikając żółty przycisk **"Pobierz Projekt (.zip)"** w grze.
2. Rozpakuj pobrany plik `cpp_dungeon_game_engine.zip` do dowolnego folderu (np. `C:\Projekty\DungeonEngine`).
3. Otwórz **Visual Studio 2022**.
4. W oknie startowym wybierz opcję:
   📁 **Otwórz folder lokalny** (*Open a local folder*).
5. Wybierz rozpakowany folder (ten, w którym bezpośrednio znajduje się plik `CMakeLists.txt`).

---

## KROK 3: Automatyczna konfiguracja CMake

1. Po otwarciu folderu Visual Studio automatycznie zauważy plik `CMakeLists.txt`.
2. W dolnym oknie **Dane wyjściowe** (*Output*) zobaczysz postęp konfiguracji CMake.
3. Plik `CMakeLists.txt` automatycznie skonfiguruje pobieranie biblioteki **Raylib 5.0** (przez mechanizm FetchContent), więc nie musisz ręcznie instalować bibliotek zewnętrznych!
4. Odczekaj chwilę, aż w dolnym oknie pojawi się napis:
   `Generowanie pamięci podręcznej CMake powiodło się` (*CMake generation finished*).

---

## KROK 4: Wybór celu i kompilacja do .exe

1. Na górnym pasku narzędzi znajdź rozwijane menu elementów startowych (obok zielonego trójkąta odtwarzania ▶).
2. Zamiast "Bieżący dokument" wybierz:
   🎯 **`dungeon_game.exe (src\dungeon_game.exe)`**
3. Obok możesz wybrać konfigurację kompilacji:
   - **`x64-Release`** (Zalecane: gra będzie działać z maksymalną prędkością 60 FPS)
   - lub **`x64-Debug`** (do debugowania i podglądu zmiennych)
4. Kliknij zielony trójkąt ▶ **Uruchom** lub wciśnij klawisz **F5** (bądź **Ctrl + F5**, aby uruchomić bez debuggera).
5. Visual Studio skompiluje silnik i uruchomi okno gry!

---

## KROK 5: Gdzie znajduje się gotowy plik .exe?

Po pomyślnej kompilacji plik wykonywalny znajduje się na Twoim dysku w folderze projektu:
```text
TwojFolderProjektu\out\build\x64-Release\dungeon_game.exe
```
Możesz skopiować ten plik `.exe` w dowolne miejsce, utworzyć do niego skrót na Pulpicie i grać bezpośrednio bez konieczności ponownego otwierania Visual Studio!

---

## ❓ Częste pytania i rozwiązywanie problemów:

- **Problem:** Visual Studio mówi, że nie odnaleziono polecenia `cmake` lub kompilatora.
  - **Rozwiązanie:** Otwórz Visual Studio Installer i upewnij się, że zaznaczony jest pakiet "Programowanie aplikacji klasycznych w języku C++" wraz z "Narzędziami CMake języka C++ dla systemu Windows".
- **Problem:** Chcę uruchomić czysty tryb konsolowy (ASCII) bez Raylib.
  - **Rozwiązanie:** W pliku `CMakeLists.txt` zmień linijkę `option(USE_RAYLIB "..." ON)` na `OFF` i zapisz plik (Ctrl+S).
