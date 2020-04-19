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


## 기본환경 설정2 (첫번째 시도) (**실패**)