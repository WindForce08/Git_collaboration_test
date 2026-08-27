### 05. 작성한 udev 규칙 2개 + 규칙 키 설명표
```
# 작성한 udev 규칙

pa31@pa31-Legion-Pro-5-16IAX10:/etc/udev/rules.d$ cat 99-robot-sensor.rules 
ATTR{diskseq}=="39", SYMLINK+="robot_lidar"
ATTR{diskseq}=="41", SYMLINK+="robot_imu"
```
> 위 04번에 따라 위와 같은 udev 규칙을 작성하였다.

#### 규칙 키 설명표
| 키 / 연산자     | 의미                     | 역할 / 예시                                          |
| ----------- | ---------------------- | ------------------------------------------------ |
| `SUBSYSTEM` | 장치가 속한 서브시스템           | `SUBSYSTEM=="block"` → 블록 장치인지 확인                |
| `KERNEL`    | 커널이 부여한 장치 이름          | `KERNEL=="loop17"` → `loop17` 장치와 매칭             |
| `ATTR{...}` | 장치의 특정 sysfs 속성값       | `ATTR{diskseq}=="39"` → `diskseq`가 39인 장치와 매칭    |
| `SYMLINK+=` | 장치에 추가적인 심볼릭 링크 이름을 부여 | `SYMLINK+="robot_lidar"` → `/dev/robot_lidar` 생성 |
| `MODE`      | 장치 파일의 권한 설정           | `MODE="0660"` → 소유자/그룹에 읽기·쓰기 권한 부여              |
| `GROUP`     | 장치 파일의 소유 그룹 지정        | `GROUP="dialout"` → `dialout` 그룹이 장치 사용          |
| `==`        | 비교 / 매칭            | `KERNEL=="loop17"` → 조건이 loop17인지 확인             |
| `=`         | 값을 설정             | `MODE="0660"` → 권한을 0660으로 설정                    |
| `+=`        | 기존 값에 추가           | `SYMLINK+="robot_lidar"` → 심볼릭 링크 이름을 추가         |
