# ceserver

# Build

  - Linux:gcc
  - Android:Android Studio(ndk-build)

The following explanation is for ceserver only.
#### Linux
・gcc

```
ceserver
│  makefile
│
├─bin
├─include
│      api.h
│      ceserver.h
│      ceservertest.h
│      context.h
│      extensionfunctions.h
│      extensionloader.h
│      porthelp.h
│      symbols.h
│      threads.h
│
└─source
        api.c
        ceserver.c
        ceservertest.c
        context.c
        extensionfunctions.c
        extensionloader.c
        porthelp.c
        symbols.c
        threads.c
```
In the above state, move to the ceserver folder and execute the `make` command.


#### Android
・Android Studio(ndk-build)

```
EXECUTABLE
 └─jni
          Android.mk
          Application.mk
```

In the above state, move to the EXECUTABLE folder with Android Studio Terminal and execute `ndk-build`.

