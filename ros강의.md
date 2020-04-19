# CH02

- Node간 통신
  - msg 파싱
  - msg 기록(센서값 저장)
    - 로봇을 돌렸을 떄 나온 데이터들
    - 이후 해당 데이터들을 가지고, 여러 알고리즘을 시뮬레이션 하여 효율을 검증해 볼 수 있다.

- Tools
  - rviz
    - 센서 Data 시각화 가능하다.
  - RQT
    - work flow 제공
    - 해당 흐름을 통해서 CLI 대신 흐름을 제어도 가능하다.
  - Gazebo (가지보)
    - 시뮬레이션 환경을 제공해준다.
    - Map, Robot의 3d 시뮬레이션

# CH03 개발환경 구축
- ROS 버전
  - `kinetic kame` + Ubuntu(LTS(long term)) 버전