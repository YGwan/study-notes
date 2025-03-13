# Ubuntu SSD mount 하는법
- 단순히 SSD을 넣는다고 바로 mount가 되는건 아니다.

<br>

## 방법

### 1. SSD 연결 확인

```bash
lsblk

&

fdisk -l
```

<br>

### 2. SSD 파티션 생성 (필요한 경우)
- SSD가 이미 포맷되어 있다면 이 단계를 건너뛸 수 있다. 
- 새 SSD라면 파티션을 생성해야 합니다.

```bash
sudo fdisk /dev/sdX
```
- 💡 sdX는 lsblk에서 확인한 SSD 이름

> fdisk /dev/sda
> Welcome to fdisk (util-linux 2.23.1).
> Changes will remain in memory only, until you decide to write them.
> Be careful before using the write command. Command (m for help):

- 실행 시 위와 같은 문구가 뜸

<br>

- ps) fdisk 사용 방법
    ```
    • n → 새 파티션 생성
    • p → 기본 파티션 선택
    • 1 → 첫 번째 파티션 선택
    • 엔터 (default 값 사용)
    • w → 변경 사항 저장 및 종료
    ```

<br>

- ps) 포맷되어 있는지 확인하는 방법
    ```bash
    lsblk -f
    ```
  - FSTYPE(파일 시스템 유형)이 표시되면 포맷된 상태입
  - 만약 FSTYPE이 비어 있다면, 포맷되지 않은 상태

<br>

### 3. 파일 시스템 생성 (포맷)
```bash
sudo mkfs.ext4 /dev/sdX1
```
- 💡 sdX1은 생성한 파티션 이름

<br>

### 4. 마운트 포인트 생성
```bash
sudo mkdir -p /mnt/sdX1
```
- 💡 sdX1는 임의로 생성한 파일명이므로 원하는 파일명으로 해도 상관 없다.

<br>

### 5. SSD 마운트
```bash
sudo mount /dev/sdX1 /mnt/ssd
```

<br>

### 6. 마운트 되었는지 확인
```bash
df -h
```


> 하지만 기본적으로 이렇게 하고 끝내면, 재부팅 시 마운트 정보가 사라짐 
> 따라서 영구적으로 적용하기 위해서는 추가적인 설정 필요

---

## 부팅 시 자동 마운트 (영구 적용)
- 자동 마운트를 위해 /etc/fstab 파일을 수정

### 1. UUID 확인
```bash
sudo blkid
```

<br>

### 2. /etc/fstab 파일 수정
```bash
# 원활한 파일 수정을 위해 vim 설치 진행
sudo apt-get install vim

sudo vim /etc/fstab
# 다음 줄 추가
UUID={UUID명} {마운트경로} {파일시스템} defaults 0 2
# ex
UUID=abcd-1234-efgh-5678 /mnt/ssd ext4 defaults 0 2
```
- defaults 첫 번째 숫자 : Dump 백업 설정
  - 0: 백업 안 함 (일반적으로 0을 사용)
  - 1: dump 명령어를 사용할 때 백업 포함 (거의 사용되지 않음)
  - 보통 시스템 백업에 사용되지 않으므로 0을 사용합니다.


- defaults 두 번째 숫자 : fsck 파일 시스템 검사 순서
  - 이 값은 fsck가 부팅 시 파일 시스템을 검사하는 순서를 결정합니다.
  - 0: 부팅 시 검사하지 않음 (네트워크 스토리지 등에서 사용)
  - 1: 루트 파일 시스템 (/) 전용 (부팅 시 가장 먼저 검사)
  - 2: 기타 파일 시스템 (일반적인 추가 디스크)
  - 일반적으로 /mnt/ssd 같은 보조 디스크는 2를 사용

<br>

### 3. 변경 사항 적용
```bash
sudo mount -a
```

<br><br><br>