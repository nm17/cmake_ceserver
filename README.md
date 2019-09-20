# cmake_ceserver
Work in progress project to add CMake to ceserver.

## Execution options
  - `-a` Perform module enumeration only for the specified process ID.
  - `-m` If `1` is specified, memory is read and written only with the ptrace privilege, not via the virtual file system.
  - `-p` Listen on the specified port number instead of the default 52736.
  - `-s` It is disassembled with the specified architecture regardless of the ceserver architecture. It is convenient to specify with Android emulator (x86 and ARM are mixed)etc. 
  - `-t` Start ceserver in test mode.

# Usage
### Linux
 - Start ceserver with administrator privileges. `sudo ./ceserver`
 - Start Cheat Engine via Wine, or if you are running Linux on a virtual machine, start Cheat Engine on the host OS.
 - Select the Network tab of the process list. In the Host field, enter localhost (via Wine) or Guest OS ip (on a virtual machine).

### Android
 - Execute `su` and start ceserver with root privileges.
 - Run the adb command on the PC. `adb forward tcp:52736 tcp:52736`
 - Start Cheat Engine.
 - Select the Network tab of the process list. In the Host field, enter localhost (Android Emulator) or Android device ip address (real Android device).
 
