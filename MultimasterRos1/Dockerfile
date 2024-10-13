FROM osrf/ros:noetic-desktop-full-focal

#ENV ROS_DISTRO noetic
ARG ROS_DISTRO=noetic

# ARG ROS_MASTER_URI=http://0.0.0.0:11311
SHELL ["/bin/bash", "-c"]

RUN apt-get update
RUN apt-get install -y ros-noetic-fkie-master-sync && \
    apt-get install -y ros-noetic-fkie-master-discovery
RUN apt-get install -y tmux tmuxinator
RUN apt-get install -y nano

# RUN echo -e "source /opt/ros/noetic/setup.bash \n" >> ~/.bashrc ;    

COPY ./src/ /root/

RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc \
    && source /opt/ros/$ROS_DISTRO/setup.bash \
    && cd ~/catkin_ws/ \
    && catkin_make \
    && echo "source /root/catkin_ws/devel/setup.bash" >> ~/.bashrc \
    && source /root/catkin_ws/devel/setup.bash

WORKDIR /root/catkin_ws
# Load ROS environment at each run

COPY ./ros_entrypoint.sh /
RUN chmod 755 /ros_entrypoint.sh
ENTRYPOINT ["/ros_entrypoint.sh"]

# CMD roscore
CMD [ "bash" ]

