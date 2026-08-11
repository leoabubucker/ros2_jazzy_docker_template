# pull the latest jazzy desktop docker for Ubuntu 24.04 (noble)
FROM osrf/ros:jazzy-desktop-full-noble

ARG USERNAME=ubuntu

# update dependencies and install development tools
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        sudo \
        git \
        build-essential \
        ros-${ROS_DISTRO}-rosbridge-suite \
        ros-${ROS_DISTRO}-web-video-server \
        npm \
        gdb \
    && rm -rf /var/lib/apt/lists/*

# modifies the existing ubuntu user, adds them to sudo and dialout groups, removes password requirement for sudo 
RUN usermod -aG sudo,dialout ${USERNAME} \
    && echo "${USERNAME} ALL=(root) NOPASSWD:ALL" \
        > /etc/sudoers.d/${USERNAME} \
    && chmod 0440 /etc/sudoers.d/${USERNAME}

# switches execution from root to ubuntu user
USER ${USERNAME}

WORKDIR /ros2-ws

# sources ros environment on launch and then attempts to source the local setup when it changes
RUN echo "source /opt/ros/jazzy/setup.bash" >> /home/${USERNAME}/.bashrc \
    && echo "if [ -f /ws/install/setup.bash ]; then source /ws/install/setup.bash; fi" \
        >> /home/${USERNAME}/.bashrc

CMD ["bash"]
