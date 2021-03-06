project(Deps VERSION 0.1 LANGUAGES C CXX)

if (WIN32 AND CMAKE_SIZEOF_VOID_P EQUAL 4)
    # Detours lib
    add_library(Detours
        Detours/src/detours.cpp
        Detours/src/disasm.cpp
        Detours/src/image.cpp
        Detours/src/modules.cpp
        )

    target_compile_definitions(Detours PRIVATE "DETOURS_X86" "DETOURS_32BIT")

    target_include_directories(Detours PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/Detours/src>
        $<INSTALL_INTERFACE:Detours/src>)

    set_property(TARGET Detours PROPERTY FOLDER "3rdParty")
    export(TARGETS Detours FILE Detours.cmake)
endif()


# EasyLogging++ lib
add_library(EasyLogging++
    EasyLogging++/EasyLogging/src/easylogging++.cc
    EasyLogging++/EasyLogging/src/easylogging++.h
    )

target_include_directories(EasyLogging++ PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/EasyLogging++/EasyLogging/src>
    $<INSTALL_INTERFACE:EasyLogging++/EasyLogging/src>)

set_property(TARGET EasyLogging++ PROPERTY FOLDER "3rdParty")
export(TARGETS EasyLogging++ FILE EasyLogging++.cmake)
