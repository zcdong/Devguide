# Simulation Debugging

As the simulation is running on the host machine, all the desktop development tools are available.

## Valgrind

<div class="host-code"></div>

```sh
brew install valgrind
```

or

<div class="host-code"></div>

```sh
sudo apt-get install valgrind
```

## GCC Toolchain (Linux)

## CLANG Toolchain (Mac OS, Linux)

### Address Sanitizer

<div class="host-code"></div>

```clang
-O1 -g -fsanitize=address -fno-omit-frame-pointer
```

## Start combinations

SITL can be launched with and without debugger attached and with either jMAVSim or Gazebo as simulation backend. This results in the start options below:

<div class="host-code"></div>

```sh
make posix_sitl_default jmavsim
make posix_sitl_default jmavsim_gdb
make posix_sitl_default jmavsim_lldb

make posix_sitl_default gazebo
make posix_sitl_default gazebo_gdb
make posix_sitl_default gazebo_lldb

make posix_sitl_lpe jmavsim
make posix_sitl_lpe jmavsim_gdb
make posix_sitl_lpe jmavsim_lldb

make posix_sitl_lpe gazebo
make posix_sitl_lpe gazebo_gdb
make posix_sitl_lpe gazebo_lldb
```
