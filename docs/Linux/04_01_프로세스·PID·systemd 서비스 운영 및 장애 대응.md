<img width="1055" height="1491" alt="image" src="https://github.com/user-attachments/assets/776a3625-c238-4a60-a175-41505730f032" />

# Linux 프로젝트 — 4장 1교시
## 프로세스·PID·systemd 서비스 운영 및 장애 대응

### 1. 프로세스(Process)란?

프로세스는 실행 중인 프로그램의 인스턴스이다.

| 개념 | 설명 |
|---|---|
| Program | 디스크에 저장된 실행 프로그램 |
| Process | 실행 중인 프로그램 |
| PID | 프로세스 식별 번호 |
| PPID | 부모 프로세스의 PID |
| systemd | Linux 시스템·서비스 관리자 |
| systemctl | systemd 서비스를 관리하는 명령어 |

### 2. 프로세스 확인 및 종료

```bash
ps -ef                   # 전체 프로세스 조회
top                      # CPU·메모리·프로세스 확인
pgrep -a sshd            # 프로세스 이름으로 검색
ps -fp 1234              # 특정 PID 상세 조회

kill -TERM 1234          # 정상 종료 요청 (SIGTERM 15)
kill -KILL 1234          # 강제 종료 (SIGKILL 9)
```

- **SIGTERM(15):** 프로세스에 정상 종료를 요청
- **SIGKILL(9):** 프로세스를 강제로 종료
- 실무에서는 SIGTERM을 먼저 사용하고, 필요할 때 SIGKILL을 검토한다.

### 3. systemd와 systemctl

systemd는 서비스 실행·중지·자동 시작·재시작 등을 관리한다.

| 명령어 | 역할 |
|---|---|
| `systemctl start` | 서비스 시작 |
| `systemctl stop` | 서비스 중지 |
| `systemctl restart` | 서비스 재시작 |
| `systemctl status` | 서비스 상태 확인 |
| `systemctl enable` | 부팅 시 자동 시작 등록 |
| `systemctl disable` | 자동 시작 해제 |
| `systemctl daemon-reload` | Unit 파일 변경 사항 반영 |

**핵심 차이**

- `start`: 지금 서비스 실행
- `enable`: 재부팅 시 자동 실행 등록
- `enable --now`: 자동 시작 등록 + 즉시 실행

### 4. systemd 서비스 직접 구축

#### ① Bash 프로그램 생성

```bash
sudo mkdir -p /opt/linux-training-ch04
sudo chown infra:infra /opt/linux-training-ch04
nano /opt/linux-training-ch04/heartbeat.sh
```

`heartbeat.sh` 내용:

```bash
#!/usr/bin/env bash

while true
do
    echo "$(date '+%F %T') [INFO] linux-lab running"
    sleep 5
done
```

```bash
chmod 750 /opt/linux-training-ch04/heartbeat.sh
bash -n /opt/linux-training-ch04/heartbeat.sh
```

#### ② Service 파일 생성

```bash
sudo nano /etc/systemd/system/linux-lab.service
```

```ini
[Unit]
Description=Linux Training Heartbeat Service
After=network.target

[Service]
Type=simple
User=infra
WorkingDirectory=/opt/linux-training-ch04
ExecStart=/usr/bin/bash /opt/linux-training-ch04/heartbeat.sh
Restart=on-failure
RestartSec=3
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

**주요 설정**

| 설정 | 의미 |
|---|---|
| `ExecStart` | 실행할 프로그램 |
| `User` | 서비스 실행 계정 |
| `Restart=on-failure` | 비정상 종료 시 자동 재시작 |
| `RestartSec=3` | 재시작 전 3초 대기 |
| `WantedBy=multi-user.target` | 부팅 자동 시작 연결 대상 |

#### ③ 서비스 등록 및 실행

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now linux-lab

systemctl status linux-lab --no-pager
systemctl is-active linux-lab
systemctl is-enabled linux-lab
```

정상 상태:

```text
active
enabled
```

### 5. 서비스 로그 확인

`journalctl`은 systemd 저널 로그를 조회하는 명령어이다.

```bash
# 최근 로그 20줄
sudo journalctl -u linux-lab -n 20 --no-pager

# 실시간 로그
sudo journalctl -u linux-lab -f

# 현재 부팅 이후 로그
sudo journalctl -u linux-lab -b --no-pager
```

| 옵션 | 설명 |
|---|---|
| `-u` | 특정 서비스 지정 |
| `-n 20` | 최근 20줄 출력 |
| `-f` | 실시간 로그 확인 |
| `-b` | 현재 부팅 이후 로그 |
| `--no-pager` | 페이지 도구 없이 출력 |

### 6. 서비스 장애 대응

**장애 상황:** 프로그램이 비정상 종료됨.

```bash
# 서비스 상태 확인
systemctl status linux-lab --no-pager

# 오류 로그 분석
sudo journalctl -xeu linux-lab --no-pager

# 서비스 설정 확인
systemctl cat linux-lab

# 실행 파일 권한 확인
ls -l /opt/linux-training-ch04/heartbeat.sh
```

#### 자동 복구 실습

```bash
# 실습용 서비스의 주 프로세스 강제 종료
sudo systemctl kill --kill-whom=main \
  --signal=SIGKILL linux-lab.service

# 자동 재시작 확인
systemctl status linux-lab --no-pager
sudo journalctl -u linux-lab -n 20 --no-pager
```

`Restart=on-failure` 설정이 있으면 systemd가 비정상 종료 후 재시작을 시도한다.

### 장애 대응 순서

1. `systemctl status` — 서비스 상태 확인
2. `journalctl` — 오류 로그 분석
3. 실행 파일·권한·설정 확인
4. 문제 수정 및 서비스 복구
5. 정상 실행·로그·PID 재검증

### 7. 핵심 명령어 요약

| 명령어 | 역할 |
|---|---|
| `ps -ef` | 프로세스 조회 |
| `top` | 자원 사용량 확인 |
| `pgrep` | 프로세스 검색 |
| `kill` | 프로세스에 시그널 전달 |
| `systemctl` | 서비스 관리 |
| `journalctl` | 서비스 로그 조회 |
| `systemctl daemon-reload` | Unit 설정 반영 |
| `systemctl enable --now` | 자동 시작 등록 및 즉시 실행 |

### 8. 면접 핵심 질문

**Q1. 프로세스와 서비스의 차이는?**

- 프로세스는 실행 중인 프로그램이다.
- 서비스는 지속적으로 기능을 제공하며 systemd 등으로 관리할 수 있다.

**Q2. systemd와 systemctl의 차이는?**

- systemd: 시스템·서비스 관리자
- systemctl: systemd를 제어하는 명령어

**Q3. Linux 서비스 장애 발생 시 대응 방법은?**

- `systemctl status`로 상태 확인
- `journalctl`로 로그 분석
- 실행 경로·설정·권한 확인
- 원인 수정 후 서비스 재시작 및 검증

---

## 최종 핵심

**Linux 운영의 기본 흐름**

프로세스 확인 → 서비스 상태 확인 → 로그 분석 → 원인 해결 → 서비스 복구

**학습 목표:** Linux 프로세스를 관리하고, systemd 서비스를 직접 등록·운영하며, 장애 발생 시 원인을 분석하고 복구할 수 있다.
