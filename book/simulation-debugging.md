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
