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

Then run Valgrind with this target:

<div class="host-code"></div>

```sh
make posix_sitl_default jmavsim___valgrind
```

## GCC Toolchain (Linux)

## CLANG Toolchain (Mac OS, Linux)

### Address Sanitizer

The Clang address sanitizer can help to find alignment (bus) errors and other memory faults like segmentation fauls. The diff below sets the right compile options.

<aside class="todo">
Add convenience target to run `make abc address-sanitizer`
</aside>

<div class="host-code"></div>

```diff
diff --git a/cmake/common/px4_base.cmake b/cmake/common/px4_base.cmake
index 26598fe..4c9177d 100644
--- a/cmake/common/px4_base.cmake
+++ b/cmake/common/px4_base.cmake
@@ -530,14 +530,14 @@ function(px4_add_common_flags)
                )
        endif()
 
-       set(max_optimization -Os)
+       set(max_optimization -O1)
 
        set(optimization_flags
                -fno-strict-aliasing
-               -fomit-frame-pointer
                -funsafe-math-optimizations
                -ffunction-sections
                -fdata-sections
+               -g -fsanitize=address -fno-omit-frame-pointer
                )
 
        if (NOT ${CMAKE_C_COMPILER_ID} MATCHES ".*Clang.*")

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
