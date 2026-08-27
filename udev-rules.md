### 05. 작성한 udev 규칙 2개 + 규칙 키 설명표
```
# 작성한 udev 규칙

pa31@pa31-Legion-Pro-5-16IAX10:/etc/udev/rules.d$ cat 99-robot-sensor.rules 
ATTR{diskseq}=="39", SYMLINK+="robot_lidar"
ATTR{diskseq}=="41", SYMLINK+="robot_imu"
```
> 위 04번에 따라 위와 같은 udev 규칙을 작성하였다.

#### 규칙 키 설명표

| 키 / 연산자 | 의미 | 역할 / 예시 |
|---|---|---|
| `SUBSYSTEM` | 장치가 속한 커널 서브시스템을 지정한다. | `SUBSYSTEM=="block"` → 블록 장치인 경우에만 규칙 적용 |
| `KERNEL` | 커널이 부여한 장치 이름을 기준으로 장치를 매칭한다. | `KERNEL=="loop18"` → 이름이 `loop18`인 장치와 매칭 |
| `ATTR{...}` | 장치의 sysfs 속성값을 기준으로 장치를 매칭한다. | `ATTR{diskseq}=="41"` → `diskseq` 값이 41인 장치와 매칭 |
| `SYMLINK+=` | 장치에 추가적인 심볼릭 링크 이름을 생성한다. | `SYMLINK+="robot_imu"` → `/dev/robot_imu` 링크 생성 |
| `MODE` | 생성되는 장치 파일의 접근 권한을 지정한다. | `MODE="0660"` → 소유자와 그룹에 읽기·쓰기 권한 부여 |
| `GROUP` | 장치 파일의 소유 그룹을 지정한다. | `GROUP="dialout"` → `dialout` 그룹이 장치에 접근 |
| `==` | 지정한 값과 일치하는지 비교하여 장치를 매칭한다. | `KERNEL=="loop18"` → 커널 이름이 `loop18`인지 확인 |
| `=` | 장치 속성이나 설정값을 지정한 값으로 설정한다. | `MODE="0660"` → 장치 권한을 `0660`으로 설정 |
| `+=` | 기존 값에 새로운 값을 추가한다. | `SYMLINK+="robot_imu"` → 기존 링크에 `robot_imu`라는 링크를 추가 |

#### udevadm info --attribute-walk /dev/loop18 확인 내용 

```
pa31@pa31-Legion-Pro-5-16IAX10:~$ udevadm info --attribute-walk /dev/loop18 Udevadm info starts with the device specified by the devpath and then walks up the chain of parent devices. It prints for every device found, all possible attributes in the udev rules key format. A rule to match, can be composed by the attributes of the device and the attributes from one single parent device. looking at device '/devices/virtual/block/loop18': KERNEL=="loop18" SUBSYSTEM=="block" DRIVER=="" ATTR{alignment_offset}=="0" ATTR{capability}=="0" ATTR{discard_alignment}=="0" ATTR{diskseq}=="41" ATTR{events}=="media_change" ATTR{events_async}=="" ATTR{events_poll_msecs}=="-1" ATTR{ext_range}=="256" ATTR{hidden}=="0" ATTR{inflight}==" 0 0" ATTR{integrity/device_is_integrity_capable}=="0" ATTR{integrity/format}=="none" ATTR{integrity/protection_interval_bytes}=="0" ATTR{integrity/read_verify}=="0" ATTR{integrity/tag_size}=="0" ATTR{integrity/write_generate}=="0" ATTR{loop/autoclear}=="0" ATTR{loop/dio}=="0" ATTR{loop/offset}=="0" ATTR{loop/partscan}=="0" ATTR{loop/sizelimit}=="0" ATTR{mq/0/cpu_list}=="0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23" ATTR{mq/0/nr_reserved_tags}=="0" ATTR{mq/0/nr_tags}=="128" ATTR{partscan}=="0" ATTR{power/async}=="disabled" ATTR{power/control}=="auto" ATTR{power/runtime_active_kids}=="0" ATTR{power/runtime_active_time}=="0" ATTR{power/runtime_enabled}=="disabled" ATTR{power/runtime_status}=="unsupported" ATTR{power/runtime_suspended_time}=="0" ATTR{power/runtime_usage}=="0" ATTR{queue/add_random}=="0" ATTR{queue/chunk_sectors}=="0" ATTR{queue/dax}=="0" ATTR{queue/discard_granularity}=="4096" ATTR{queue/discard_max_bytes}=="4294966784" ATTR{queue/discard_max_hw_bytes}=="4294966784" ATTR{queue/discard_zeroes_data}=="0" ATTR{queue/dma_alignment}=="511" ATTR{queue/fua}=="0" ATTR{queue/hw_sector_size}=="512" ATTR{queue/io_poll}=="0" ATTR{queue/io_poll_delay}=="-1" ATTR{queue/iostats}=="1" ATTR{queue/logical_block_size}=="512" ATTR{queue/max_discard_segments}=="1" ATTR{queue/max_hw_sectors_kb}=="1280" ATTR{queue/max_integrity_segments}=="0" ATTR{queue/max_sectors_kb}=="1280" ATTR{queue/max_segment_size}=="65536" ATTR{queue/max_segments}=="128" ATTR{queue/minimum_io_size}=="512" ATTR{queue/nomerges}=="0" ATTR{queue/nr_requests}=="128" ATTR{queue/nr_zones}=="0" ATTR{queue/optimal_io_size}=="0" ATTR{queue/physical_block_size}=="512" ATTR{queue/read_ahead_kb}=="128" ATTR{queue/rotational}=="0" ATTR{queue/rq_affinity}=="1" ATTR{queue/scheduler}=="[none] mq-deadline " ATTR{queue/stable_writes}=="0" ATTR{queue/virt_boundary_mask}=="0" ATTR{queue/wbt_lat_usec}=="75000" ATTR{queue/write_cache}=="write back" ATTR{queue/write_same_max_bytes}=="0" ATTR{queue/write_zeroes_max_bytes}=="4294966784" ATTR{queue/zone_append_max_bytes}=="0" ATTR{queue/zone_write_granularity}=="0" ATTR{queue/zoned}=="none" ATTR{range}=="1" ATTR{removable}=="0" ATTR{ro}=="0" ATTR{size}=="20480" ATTR{stat}==" 68 0 1344 1 0 0 0 0 0 0 1 0 0 0 0 0 0" ATTR{trace/act_mask}=="disabled" ATTR{trace/enable}=="0" ATTR{trace/end_lba}=="disabled" ATTR{trace/pid}=="disabled" ATTR{trace/start_lba}=="disabled"
```