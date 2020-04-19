# ROS with Docker
## c.f Docker

- build & Dockerfile
  - Dockerfile 세팅해 맞게 이미지 생성
- run -it
  - 컨테이너 생성 및 실행
- start
  - 컨테이너 실행

- 컨테이너 터미널 실행 하고 싶다면
  1. docker start <컨테이너>
  2. `docker exec -it <컨테이너> bash`

- docker rename <컨테이너> 이름
- docker commit <컨테이너> <이미지>

## 기본환경 설정 (첫번째 시도) (**실패**)
> [참조사이트](https://medium.com/@rookiecj/%EA%B0%91%EC%9E%90%EA%B8%B0-ros-%EA%B7%B8%EB%A6%AC%EA%B3%A0-docker%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-5b941c9ff098)
1. Dockerfile 생성
2. `docker build --build-arg HOST_USER=$USER --tag 'minkj1992/kinetic:dev' .`
```bash
Step 25/33 : ADD initial-workspace.sh $HOME/
ADD failed: stat /var/lib/docker/tmp/docker-builder201427599/initial-workspace.sh: no such file or directory

```
- 계속 위와 같은 에러가 발생하여 포기하고 docker ros를 pull한다.
1. "kinetic:dev" .` 실행 (현재 폴더 루트에서)


## 기본환경 설정2
1. docker pull ros
2. docker run -it ros


## 기본환경 설정3

1. docker pull ubuntu:18.04
2. docker run -it ubuntu
3. sudo install
```bash
apt-get update && \
      apt-get -y install sudo
```
4. lsb_release install
```
apt-get update && apt-get install -y lsb-release && apt-get clean all
```
5. ROS setting
```bash
# http://wiki.ros.org/kinetic/Installation/Ubuntu

sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

sudo apt-get update

```

## 기본환경 설정 3
1. docker pull mjenz/ros-kinetic-desktop-full
2. 


wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_kinetic.sh && chmod 755 ./install_ros_kinetic.sh & bash ./install_ros_kinetic.sh

alias eb ='vim ~/.bashrc'
alias sb ='source ~/.bashrc'
alias cw ='cd ~/catkin_ws'
alias cs ='cd ~/catkin_ws/src'
alias cm='cd ~/catkin_ws && catkin_make'
source /opt/ros/kinetic/setup.bash
source ~/catkin_ws/devel/setup.bash
export ROS_MASTER_URI=http://localhost:11311
export ROS_HOSTNAME=localhost
#export ROS_MASTER_URI=http://192.168.1.100:11311
#export ROS_HOSTNAME=192.168.1.100

## 기본환경 설정 4 ( local ) (x)
- 그냥 로컬 환경에 ros 만들자

1. wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_kinetic.sh
&& chmod 755 ./install_ros_kinetic.sh

2. bash ./install_ros_kinetic.sh
3. 이것두 하다 보니 18.04인 환경과 세팅값이 맞지 않는다.

## 기본환경 설정 5

- ubuntu16.04 기본 설정
  1. docker pull ubuntu:16.04
  2. docker run -it ubuntu:16.04
  3. docker rename great_williamson my_ros_ubuntu_16.04
  4. apt-get update && apt-get -y install sudo
  5. apt-get update && apt-get install -y lsb-release && apt-get clean all
  6. sudo apt install wget

- `ros`기본 설정
  1. touch ./install_ros_kinetic.sh
  2. wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_kinetic.sh
  3.  chmod 755 ./install_ros_kinetic.sh
  4.  bash ./install_ros_kinetic.sh

- `docker image화`
  1. docker commit my_ros_ubuntu_16.04 minkj1992/my_ros_ubuntu:base
  2. docker push minkj1992/my_ros_ubuntu:base


- 실행법
  - terminator를 설치하고 사용한다.
  1. docker start my_ros_base
  2. docker exec -it my_ros_base bash

- 실습
  - roscore
  - rosrun turtlesim turtlesim_node
  - rosrun turtlesim turtle_teleop_key
  - rosrun rqt_graph rqt_graph

**엄청난 문제가 발견되었다. 멀티 프로세싱을 해주어야 하는데 docker는 기본적으로 단일 프로세스 안에서 컨테이너를 돌린다. core dump가 일어난다.** ...
