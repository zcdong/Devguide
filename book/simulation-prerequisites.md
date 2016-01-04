# Simulation Introduction

PX4 officially supports two simulation backends: [jMAVSim](simulation-sitl.md), a lightweight and basic Java simulator and [Gazebo](simulation-gazebo.md), a fully-featured robotics simulation engine. Both simulators run on Mac OS and Linux.

## Installing Prerequisites

### Mac OS

<div class="host-code"></div>

```sh
brew install ant graphviz sdformat3 protobuf eigen
```

### Linux


<div class="host-code"></div>

```sh
sudo apt-get install ant protobuf-compiler libeigen3-dev openjdk-7-jdk openjdk-7-jre
```

### Windows

  * If Java is not already installed, install according to the [Oracle Java installation instructions](https://java.com/en/download/help/windows_manual_download.xml).
  
