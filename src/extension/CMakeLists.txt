if (${CMAKE_SYSTEM_PROCESSOR} MATCHES "aarch64")
    message(FATAL_ERROR "aarch64 is not supported by ceserver")
else()
    add_library(ceserver-extension SHARED server.c server.h speedhack.c speedhack.h)

    target_link_libraries(ceserver ceserver-extension)
endif()