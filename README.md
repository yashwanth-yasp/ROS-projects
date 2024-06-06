# ROS-projects



- http://wiki.ros.org/docker/Tutorials/Docker
- Video reference - https://youtu.be/qWuudNxFGOQ?si=8anqLM4pdfq0hWtJ

```bash
docker pull osrf/ros:melodic-desktop
```

```bash
docker run -it osrf/ros:melodic-desktop
```

- **The following is for linux systems as you need to specify while starting a container for the gui support**
- **Run docker bash file**

```bash
# If not working, first do: sudo rm -rf /tmp/.docker.xauth
# It still not working, try running the script as root.
## Build the image first
### docker build -t r2_path_planning .
## then run this script
xhost local:root


XAUTH=/tmp/.docker.xauth


docker run -it \
    --name=docker_container\
    --env="DISPLAY=$DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --env="XAUTHORITY=$XAUTH" \
    --volume="$XAUTH:$XAUTH" \
    --net=host \
    --privileged \
    osrf/ros:melodic-desktop \
    bash

echo "Done."
```

- **Run docker gpu file**

```bash
# If not working, first do: sudo rm -rf /tmp/.docker.xauth
# It still not working, try running the script as root.
## Build the image first
### docker build -t r2_path_planning .
## then run this script
xhost local:root


XAUTH=/tmp/.docker.xauth

docker run -it \
    --name=r2_pathplanning_container \
    --env="DISPLAY=$DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --env="XAUTHORITY=$XAUTH" \
    --volume="$XAUTH:$XAUTH" \
    --net=host \
    --privileged \
    --runtime=nvidia \
    osrf/ros:melodic-desktop \
    bash

echo "Done."
```

- **As we are working with the docker, each terminal and node you create you have to create a new container, you can use the new bash file below, it takes an argument as the docker container name**

```bash
# If not working, first do: sudo rm -rf /tmp/.docker.xauth
# It still not working, try running the script as root.
## Build the image first
### docker build -t r2_path_planning .
## then run this script
xhost local:root


XAUTH=/tmp/.docker.xauth


docker run -it \
    --name=$1\
    --env="DISPLAY=$DISPLAY" \
    --env="QT_X11_NO_MITSHM=1" \
    --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" \
    --env="XAUTHORITY=$XAUTH" \
    --volume="$XAUTH:$XAUTH" \
    --net=host \
    --privileged \
    osrf/ros:melodic-desktop \
    bash

echo "Done."
```

```bash
./run_docker.bash <container_name>
```

# Restarting the docker container 

```bash
docker restart <container_name>
```

```bash
docker exec -it <container_name> bash
```
# User permission error docker 

```bash
 sudo chmod 666 /var/run/docker.sock
```

