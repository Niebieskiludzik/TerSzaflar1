cmake_minimum_required(VERSION 3.20)
project(DungeonEngineCPP VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

include_directories(include)


# Zbierz wszystkie pliki źródłowe z folderu src/
file(GLOB_RECURSE SOURCES
    src/main.cpp
    src/GameEngine.cpp
    src/IRender.cpp
    src/DungeonMap.cpp
    src/OpenGLRender.cpp
    src/RayLibRender.cpp
    src/EntityManager.cpp
    src/ConsoleRenderer.cpp
)

add_executable(dungeon_game ${SOURCES})

# Optymalizacja kompilatora
# Flagi optymalizacji i ostrzeżeń
if(MSVC)
    # /W4 daje wysoki poziom ostrzeżeń, a /RTC1 pozostaje dla Debug
    target_compile_options(dungeon_game PRIVATE /W4)
    
    # /O2 włączamy TYLKO w konfiguracji Release
    target_compile_options(dungeon_game PRIVATE $<$<CONFIG:Release>:/O2>)
else()
    target_compile_options(dungeon_game PRIVATE -Wall -Wextra)
    target_compile_options(dungeon_game PRIVATE $<$<CONFIG:Release>:-O3>)
endif()