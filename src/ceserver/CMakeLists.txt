add_executable(ceserver
        api.c
        api.h
        ceserver.c
        ceserver.h
        selftest/ceservertest.c
        selftest/ceservertest.h
        utils/context.c
        utils/context.h
        extension/extensionfunctions.h
        extension/extensionfunctions.c
        extension/extensionloader.c
        extension/extensionloader.h
        utils/porthelp.c
        utils/porthelp.h
        utils/symbols.c
        utils/symbols.h
        utils/threads.c
        utils/threads.h
        )

if (OS_ANDROID)
    message(VERBOSE "OS_ANDROID = 1")
    target_link_options(ceserver PUBLIC -llog) # Fix for Android logging
endif()