# test of multimaster

source "/opt/ros/noetic/setup.bash"
export ROS_HOSTNAME=dry

echo -e "export ROS_HOSTNAME=uav_1 \n" >> ~/.bashrc ;
source ~/.bashrc

rostopic pub rb1_topic std_msgs/String "hello there"

rosrun fkie_master_discovery master_discovery

rosrun fkie_master_sync master_sync

# access to uav

docker exec -ti multimasterros1-robot2-1 /bin/bash
docker exec -ti multimasterros1-robot1-1 /bin/bash
docker exec -ti multimasterros1-server-1 /bin/bash

# tmuxinator

tmuxinator start test

# references

https://github.com/ahrakos/ros-docker/blob/master/docker-compose.yaml
https://hackmd.io/@octobotics/rknm7a6ys#FKIE-Multimaster
https://github.com/alvcaballero/onboard_dji/blob/M300-mediaMan/launch/atlas.launch
