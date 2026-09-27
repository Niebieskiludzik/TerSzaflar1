# C++ Dungeon Game Engine

Podstawowa, modułowa gra komputerowa w języku C++20, zaprojektowana specjalnie tak, aby można było łatwo podmieniać i rozwijać warstwę graficzną:
1. **Tryb 1: Konsola ASCII** (Zero zależności, kompiluje się na każdym komputerze).
2. **Tryb 2: Raylib 2D** (Zalecane na start: kafelki, sprite'y, dźwięk, płynne 60 FPS).
3. **Tryb 3: 2.5D Raycasting** (Styl Wolfenstein 3D / DOOM).
4. **Tryb 4: Nowoczesny OpenGL 3.3+ / Vulkan** (Własne shadery GLSL, matryce MVP, oświetlenie PBR).

---

## 🖥️ Kompilacja w Visual Studio 2022 (Najprostsza metoda na Windows)

Projekt posiada gotowy plik `CMakeLists.txt`, który Visual Studio 2022 obsługuje natywnie w 100%!

1. **Wypakuj archiwum ZIP** do dowolnego folderu (np. `C:\Projekty\DungeonEngine`).
2. Uruchom **Visual Studio 2022**.
3. Upewnij się, że w *Visual Studio Installerze* masz zainstalowany składnik **"Programowanie aplikacji klasycznych w języku C++"** (*Desktop development with C++*).
4. W oknie powitalnym kliknij **"Otwórz folder lokalny"** (*Open a local folder*) i wskaż rozpakowany katalog.
5. Visual Studio automatycznie wykryje CMake i skonfiguruje projekt (w dolnym oknie Output pojawi się informacja o pobraniu biblioteki Raylib).
6. Na górnym pasku wybierz:
   - Cel: **`dungeon_game.exe`**
   - Konfigurację: **`x64-Release`** (lub `x64-Debug`)
7. Naciśnij zielony przycisk ▶ **Uruchom** (lub klawisz **F5** / **Ctrl+F5**).
8. Gotowy plik wykonywalny `dungeon_game.exe` znajdziesz w folderze:
   `out/build/x64-Release/dungeon_game.exe`

---

## 🛠️ Alternatywna kompilacja z konsoli (CMake CLI)

### Krok 1: Utworzenie katalogu build
```bash
mkdir build
cd build
```

### Krok 2: Konfiguracja i budowanie (CMake)
```bash
# Konfiguracja z automatycznym pobraniem Raylib przez FetchContent:
cmake .. -DUSE_RAYLIB=ON

# Kompilacja:
cmake --build . --config Release
```

### Krok 3: Uruchomienie pliku .exe
```powershell
# Windows:
.\Release\dungeon_game.exe
```

---

## 🚀 Jak krok po kroku dodawać zaawansowaną grafikę?

### Krok 1: Wzorzec Architektoniczny `IRenderer`
Logika gry (pozycja gracza, punkty zdrowia, algorytmy potworów) znajduje się w `GameEngine.cpp` i NIE zależy od żadnej biblioteki graficznej!
Silnik jedynie wywołuje metody z interfejsu:
```cpp
m_renderer->drawMap(...);
m_renderer->drawEntities(...);
m_renderer->drawLighting(...);
```

### Krok 2: Dodawanie tekstur i animacji
W pliku `RaylibRenderer.cpp`:
- Załaduj teksturę: `Texture2D wallTex = LoadTexture("assets/wall.png");`
- Zastąp `DrawRectangle` funkcją `DrawTextureRec(wallTex, ...)`.

### Krok 3: Dodawanie cieni i oświetlenia 2D
- Użyj bufora `RenderTexture2D lightMap = LoadRenderTexture(w, h);`.
- Narysuj czarną warstwę z otworami na pochodnie w trybie `BLEND_SUBTRACT_COLORS`.

### Krok 4: Przejście do pełnego 3D
- Skorzystaj z klasy `Camera3D` w Raylib lub własnych macierzy MVP w `OpenGLRenderer.cpp`.
- Zastąp rysowanie kafelków generowaniem siatek 3D (`DrawCube` lub modele `.obj`).
