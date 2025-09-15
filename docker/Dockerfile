FROM osrf/ros:humble-desktop-full

# install setup
RUN apt-get update

# install apps
RUN apt-get install -y \
 vim \ 
 wget \
 terminator \
 iputils-ping  \
 iproute2 \
 nmap \
 lsb-release \
 software-properties-common \
 gnupg

 # install ros additions
RUN apt-get install -y \
 ros-humble-xacro \
 ros-humble-ros2-control \
 ros-humble-ros2-controllers \
 ros-humble-joint-state-publisher-gui \
 ros-humble-rmw-cyclonedds-cpp \
 ros-humble-rosidl-generator-dds-idl

# install clang tools
RUN wget https://apt.llvm.org/llvm.sh && chmod +x llvm.sh && ./llvm.sh 18 all
RUN update-alternatives --install /usr/bin/clangd clangd /usr/bin/clangd-18 100 \
    && update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-18 100 \
    && update-alternatives --install /usr/bin/clang clang /usr/bin/clang-18 100 \
    && update-alternatives --install /usr/bin/clang-tidy clang-tidy /usr/bin/clang-tidy-18 100 \
    && update-alternatives --install /usr/bin/run-clang-tidy run-clang-tidy /usr/bin/run-clang-tidy-18 100
ENV CC=/usr/bin/clang-18
ENV CXX=/usr/bin/clang++-18

# user setup
ARG USERNAME=kann
ARG USER_UID=1000
ARG USER_GID=${USER_UID}
RUN groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd -s /bin/bash --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} \
    && mkdir /home/${USERNAME}/.config && chown ${USER_UID}:${USER_GID} /home/${USERNAME}/.config

# setup sudo
RUN apt-get update \
    && apt-get install -y sudo \
    && echo ${USERNAME} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME} \
    && rm -rf /var/lib/apt/lists/*


# copy files and folders from host to container
COPY entrypoint.sh /entrypoint.sh
RUN chmod 777 /entrypoint.sh
COPY bashrc /home/${USERNAME}/.bashrc

WORKDIR /home/${USERNAME}
RUN git clone https://github.com/unitreerobotics/unitree_ros2
RUN chown -R ${USER_UID}:${USER_GID} /home/${USERNAME}/unitree_ros2

USER root
ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
CMD ["bash"]

# cleanup
RUN rm -rf /var/lib/apt/lists/*