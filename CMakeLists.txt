cmake_minimum_required(VERSION 3.8)
project(solar_system)

set(CMAKE_CXX_STANDARD 11)

set(SOURCE_FILES
        config.h
        game.cpp
        game.h
        main.cpp
        mainmenu.cpp
        mainmenu.h
        planet.cpp
        planet.h
        scene.h
        sidebar.cpp
        sidebar.h spaceship.cpp spaceship.h resource.cpp resource.h widget.cpp widget.h widget_list.cpp widget_list.h planet_relationships.cpp planet_relationships.h)

add_executable(solar_system ${SOURCE_FILES})

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake_modules")
find_package(SFML REQUIRED system window graphics)

if (SFML_FOUND)
    include_directories(${SFML_INCLUDE_DIR})
    target_link_libraries(solar_system ${SFML_LIBRARIES})
endif()

# Prepare "Catch" library for other executables
set(CATCH_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/catch)
add_library(Catch INTERFACE)
target_include_directories(Catch INTERFACE ${CATCH_INCLUDE_DIR})

# Make test executable
set(TEST_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/test/planet_tests.cpp)
add_executable(tests ${TEST_SOURCES})
target_link_libraries(tests Catch)
