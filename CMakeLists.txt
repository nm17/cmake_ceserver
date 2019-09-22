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

add_subdirectory(src/ceserver/)

target_link_libraries(ceserver ${CMAKE_THREAD_LIBS_INIT} ${ZLIB_LIBRARIES} ${CMAKE_DL_LIBS})

message("Checking if we are compiling for Android")
if(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    set(OS_LINUX 1)
    # check if we're building natively on Android (TERMUX)
    EXECUTE_PROCESS( COMMAND uname -o COMMAND tr -d '\n' OUTPUT_VARIABLE OPERATING_SYSTEM)
    if(${OPERATING_SYSTEM} MATCHES "Android")
        set(OS_ANDROID 1)
    endif(${OPERATING_SYSTEM} MATCHES "Android")
    # Another test, in case we're cross-compiling for Android and CMAKE_SYSTEM_NAME has been set manually (as suggest by cmake)
    # https://cmake.org/cmake/help/v3.8/manual/cmake-toolchains.7.html#cross-compiling-for-android
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Android")
    set(OS_ANDROID 1)
    set(OS_LINUX 1)
else()
    set(OS_ANDROID 0)
    set(OS_LINUX 0)
endif()



if (COMPILE_WITH_EXTENSIONS)
    message(AUTHOR_WARNING "Using extensions can freeze your system, be warned.")

    add_subdirectory(src/extension/)
endif ()
