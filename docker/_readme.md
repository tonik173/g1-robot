### Readme

```sh
# in host
docker compose build
docker compose up -d
docker exec -itd docker-ros2-humble-1 terminator

# in Terminator
RUN cd unitree_ros2/cyclonedds_ws
RUN source /opt/ros/humble/setup.bash
RUN colcon build
RUN unitree_ros2/cyclonedds_ws/install/setup.bash"
```
