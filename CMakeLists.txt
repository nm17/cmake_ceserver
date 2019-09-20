cmake_minimum_required(VERSION 3.14)
project(ceserver C)

set(CMAKE_C_STANDARD 11)

include_directories(.)
include_directories(extension)

find_package(ZLIB REQUIRED)

find_package(Threads REQUIRED)

file(GLOB CESERVER_SRC src/* )

add_executable(ceserver ${CESERVER_SRC})

target_link_libraries(ceserver ${CMAKE_THREAD_LIBS_INIT} ${ZLIB_LIBRARIES} ${CMAKE_DL_LIBS})
