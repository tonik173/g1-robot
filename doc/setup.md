## Setup

### Ubuntu 24.04

```sh
sudo apt update
sudo apt upgrade
sudo apt install cmake g++ build-essential
sudo apt install libyaml-cpp-dev libeigen3-dev
sudo apt install libglfw3-dev libxinerama-dev libxcursor-dev libxi-dev
sudo apt install libboost-all-dev libspdlog-dev libfmt-dev
```

### macOS - work in progress, not working yet

On macOS, cyclone-dds is not available for brew. It has to be compiled (first the C foundation, then the C++ wrapper).

```sh
brew install yaml-cpp eigen glfw libxinerama libxcursor
```

### SDK

```sh
# clone
cd $HOME/github
git clone https://github.com/unitreerobotics/unitree_sdk2.git
cd unitree_sdk2

# build
cmake -S . -B build -DCMAKE_INSTALL_PREFIX=/opt/unitree_robotics
cd build
make

# install libraries
sudo make install

# bug fix
sudo vi /opt/unitree_robotics/include/unitree/dds_wrapper/robots/g1/g1_sub.h
# remove or comment out line 15: #include <unitree/idl/hg/SportModeState_.hpp>
```

### Mujoco simulation

```sh
# clone
cd $HOME/github
# ---- versions above 3.2.7 have breaking changes for the unitree_mujoco.git
git clone  https://github.com/google-deepmind/mujoco.git
cd mujoco
git checkout 3.2.7

# build
cmake -S . -B build
cd build
make

# install
sudo make install

# test
simulate
```

### Unitree Mujoco simulation

```sh
# clone
cd $HOME/github
git clone https://github.com/unitreerobotics/unitree_mujoco.git
# or use the fork: git clone git@github.com:tonik173/unitree_mujoco.git
# which fixes a bug: add #include <cstdint> to file unitree_mujoco\simulate\src\joystick\jstest.cc

# build
cd unitree_mujoco/simulate
cmake -S . -B build
cd build
make

# test
./unitree_mujoco

# open another terminal
cd unitree_mujoco/example/cpp
cmake -S . -B build
cd build
make

# test
./stand_go2
```

See also [Simulation](simulation.md)
