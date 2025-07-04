# Panda FER with ROS2

Clone the repo with the `--recursive` flag:

```
git clone --recursive <url>
```

This will include the [`franka_ros2` submodule](https://github.com/ivrolan/franka_ros2.git). This modifies the [franka_ros2 from mcbed](https://github.com/mcbed/franka_ros2.git) and fixes some problems with the `warehouse_ros` dependencies.

## Docker setup

If you make any changes or if it is the first time you create it, you can build the docker with:

```
sudo docker build -t "bimanual:franka" ./
```

Then you can start the container with:

```
xhost +; sudo docker compose -f docker-compose.yml up
```

You should see and output like this:

```
access control disabled, clients can connect from any host
[+] Running 1/1
 ✔ Container realtime_humble  Recreated      0.4s 
Attaching to realtime_humble
```

Finally, in another terminal, to enter the container:

```
sudo docker exec -it realtime_humble bash
```

## Using this container

You would need to do, as it is not yet defined in the Dockerfile:

```
cd ~/humble_ws
rosdep install -i --from-path src --rosdistro humble -y --skip-keys "ros-humble-libfranka"
```

You can build with

```
cd ~/humble_ws
colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release
```

Remember to source the workspace:

```
source ~/humble_ws/install/setup.bash
```

