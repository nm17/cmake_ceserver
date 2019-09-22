cmake_minimum_required(VERSION 3.14)
project(ceserver C)

set(CMAKE_C_STANDARD 11)

include_directories(.)
include_directories(extension)

message(AUTHOR_WARNING "This project is in development. Dont use for production.")

option(COMPILE_WITH_EXTENSIONS
        "Builds and links extensions to ceserver.
        Currently REALLY unstable. Most likely to freeze your system."
        OFF)

find_package(ZLIB REQUIRED)

find_package(Threads REQUIRED)

add_executable(ceserver
        src/ceserver/api.c
        src/ceserver/api.h
        src/ceserver/ceserver.c
        src/ceserver/ceserver.h
        src/ceserver/selftest/ceservertest.c
        src/ceserver/selftest/ceservertest.h
        src/ceserver/utils/context.c
        src/ceserver/utils/context.h
        src/ceserver/extension/extensionfunctions.c
        src/ceserver/extension/extensionfunctions.h
        src/ceserver/extension/extensionloader.c
        src/ceserver/extension/extensionloader.h
        src/ceserver/utils/porthelp.c
        src/ceserver/utils/porthelp.h
        src/ceserver/utils/symbols.c
        src/ceserver/utils/symbols.h
        src/ceserver/utils/threads.c
        src/ceserver/utils/threads.h
        )

target_link_libraries(ceserver ${CMAKE_THREAD_LIBS_INIT} ${ZLIB_LIBRARIES} ${CMAKE_DL_LIBS})

if (COMPILE_WITH_EXTENSIONS)
    message(AUTHOR_WARNING "Using extensions can freeze your system, be warned.")

    add_library(ceserver-extension SHARED
            src/extension/server.c
            src/extension/server.h
            src/extension/speedhack.c
            src/extension/speedhack.h
            )

    target_link_libraries(ceserver ceserver-extension)
endif ()
