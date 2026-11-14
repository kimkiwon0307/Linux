
# Linux 프로젝트 — 1장 2교시
## Ubuntu Server 24.04 LTS 설치 및 초기 환경 구축

- **학습 과정:** Linux 프로젝트 14장 30교시
- **실습 환경:** VMware Workstation + Ubuntu Server 24.04 LTS
- **학습 상태:** ✅ 완료
- **확인문제:** 5문제 중 5문제 정답 (100점)

---

## 1. 이번 교시의 목표

VMware를 이용해 Ubuntu Linux 서버를 직접 구축하고, 초기 환경을 설정한 후 정상 동작을 확인한다.

### 구축한 서버

| 항목 | 설정 |
|---|---|
| VM 이름 | linux01 |
| 운영체제 | Ubuntu Server 24.04 LTS |
| CPU | 2 vCPU |
| RAM | 4GB |
| Disk | 40GB |
| Network | NAT |
| IP 할당 | DHCP |
| Hostname | linux01 |
| Username | infra |
| SSH | OpenSSH Server 설치 |

---

## 2. VMware에서 서버 자원을 설정하는 이유

가상머신은 Host 컴퓨터의 물리 자원을 이용해 실행된다.

| 자원 | 역할 | 부족할 경우 |
|---|---|---|
| CPU | 프로그램의 명령 실행 | 처리 지연 및 성능 저하 |
| RAM | 실행 중인 데이터 저장 | 메모리 부족, OOM 가능 |
| Disk | OS·프로그램·로그 저장 | 파일 저장 실패 및 서비스 장애 |
| Network | 서버 간 통신 | SSH·웹 접속 장애 |

### 이번 사양을 선택한 이유

- 2 vCPU: 기본 서버 운영과 Nginx 실습에 적합한 출발점
- RAM 4GB: Ubuntu와 관리 프로그램 실행을 위한 여유 확보
- Disk 40GB: OS·로그·프로그램·실습 파일 저장
- NAT: VMware 가상 네트워크를 통해 외부 통신 구성

**핵심:** 서버 자원은 무조건 많이 할당하는 것이 아니라 예상 작업량과 호스트 자원을 고려하여 결정한다.

---

## 3. ISO 파일이란?

ISO는 운영체제 설치에 필요한 파일을 담은 디스크 이미지이다.

VMware에서는 ISO 파일을 가상 CD/DVD에 연결하여 운영체제를 설치한다.

### 사용한 설치 이미지

`ubuntu-24.04.5-live-server-amd64.iso`

- `ubuntu`: 운영체제 배포판
- `24.04.5`: Ubuntu 24.04 LTS 계열 설치 이미지 버전
- `live-server`: 서버 설치 이미지
- `amd64`: 64비트 x86 아키텍처
- `.iso`: 디스크 이미지 형식

Ubuntu Server는 기본적으로 GUI가 없는 서버 중심 환경이므로 CLI 및 SSH 운영 학습에 적합하다.

---

## 4. NAT와 DHCP

### NAT (Network Address Translation)

네트워크 주소 변환 기술이다.

VMware NAT 환경에서는 가상머신이 VMware의 가상 네트워크와 주소 변환 기능을 통해 외부 네트워크와 통신할 수 있다.

### DHCP (Dynamic Host Configuration Protocol)

클라이언트에 IP 주소 등의 네트워크 설정을 자동으로 제공하는 기술이다.

DHCP를 통해 제공할 수 있는 정보:

- IP 주소
- 서브넷 마스크
- 기본 게이트웨이
- DNS 서버

### NAT와 DHCP의 차이

- NAT: 네트워크 주소를 변환하여 통신을 지원한다.
- DHCP: IP 주소 등의 설정 정보를 자동으로 할당한다.

**핵심:** NAT는 주소 변환, DHCP는 네트워크 설정 자동 할당이다.

---

## 5. Ubuntu Server 설치 과정

### VMware 가상머신 생성

1. New Virtual Machine 선택
2. Typical 선택
3. I will install the operating system later 선택
4. Guest OS: Linux / Ubuntu 64-bit
5. VM 이름: linux01
6. 가상 디스크 40GB 설정
7. CPU 2 vCPU / RAM 4GB 설정
8. Network Adapter: NAT
9. Ubuntu Server ISO 연결
10. VM 전원 실행

### Ubuntu 설치 주요 설정

| 항목 | 설정 |
|---|---|
| Language | English |
| Keyboard | English (US) |
| Installation Type | Ubuntu Server |
| Network | DHCP |
| Proxy | 설정하지 않음 |
| Archive Mirror | 기본값 |
| Storage | Use an entire disk |
| LVM | 사용하지 않음 |
| SSH | Install OpenSSH Server |
| Username | infra |
| Hostname | linux01 |

### LVM을 사용하지 않은 이유

LVM(Logical Volume Manager)은 디스크 공간을 유연하게 관리하는 기술이다.

이번에는 기본 파일시스템과 디스크 구조를 먼저 익히고, 5장에서 별도 디스크를 추가하여 LVM을 직접 구성한다.

---

## 6. Hostname과 Username의 차이

- Hostname: 서버를 구별하는 이름
- Username: 서버에 로그인하는 사용자 계정

예시:

`infra@linux01:~$`

- `infra`: 현재 사용자
- `linux01`: 서버 이름
- `~`: 사용자 홈 디렉터리
- `$`: 일반 사용자 셸 프롬프트

---

## 7. 설치 후 기본 확인 명령어

### 7-1. 사용자·OS·커널 확인

```bash
whoami
hostname
cat /etc/os-release
uname -r
```

| 명령어 | 의미 |
|---|---|
| whoami | 현재 사용자 확인 |
| hostname | 서버 호스트명 확인 |
| cat /etc/os-release | OS 배포판 정보 확인 |
| uname -r | 실행 중인 커널 버전 확인 |

**중요:** Ubuntu 배포판 버전과 Linux 커널 버전은 서로 다르다.

### 7-2. CPU·메모리·디스크 확인

```bash
nproc
free -h
lsblk
df -h /
```

| 명령어 | 의미 |
|---|---|
| nproc | 사용 가능한 논리 CPU 개수 |
| free -h | 메모리 사용량 |
| lsblk | 디스크 및 파티션 구조 |
| df -h / | 루트 파일시스템 용량 |

옵션 설명:

- `-h`: 사람이 읽기 쉬운 단위로 출력
- `/`: Linux의 루트 디렉터리
- `df`: 파일시스템 용량 확인
- `lsblk`: 블록 장치 목록 확인

### 7-3. 네트워크 및 SSH 확인

```bash
ip -br addr
systemctl is-active ssh
```

- `ip -br addr`: 네트워크 인터페이스와 IP 주소를 간략하게 출력
- `systemctl is-active ssh`: SSH 서비스 실행 여부 확인

SSH 서비스가 정상 실행 중이면 `active`가 출력된다.

---

## 8. Ubuntu 초기 패키지 업데이트

### 실행 명령어

```bash
sudo apt update
sudo apt upgrade
```

### 명령어 의미

| 구문 | 의미 |
|---|---|
| sudo | 허용된 관리자 권한으로 명령 실행 |
| apt | Ubuntu 패키지 관리 도구 |
| update | 최신 패키지 목록 갱신 |
| upgrade | 설치된 패키지 업그레이드 |

### update와 upgrade의 차이

**apt update**
- 저장소의 최신 패키지 정보를 가져온다.
- 설치된 프로그램 자체를 업그레이드하지 않는다.

**apt upgrade**
- 설치된 패키지를 가능한 범위에서 최신 버전으로 업그레이드한다.

**핵심:** update는 목록 갱신, upgrade는 실제 패키지 업그레이드이다.

운영 서버에서는 업그레이드가 서비스에 미치는 영향을 검토한 후 적용해야 한다.

---

## 9. 서버 시간대 설정

### 명령어

```bash
sudo timedatectl set-timezone Asia/Seoul
timedatectl
```

### 설정 이유

서버 로그의 시간과 실제 장애 발생 시각을 비교하기 위해 시간 설정이 중요하다.

- `set-timezone`: 시스템 시간대 변경
- `Asia/Seoul`: 한국 시간대
- `timedatectl`: 현재 시간 및 시간대 설정 확인

시간대 설정과 시간 동기화는 서로 다른 기능이다.

---

## 10. 스냅샷(Snapshot)

스냅샷은 가상머신의 상태를 특정 시점으로 되돌릴 수 있도록 하는 기능이다.

### 생성 경로

VMware → VM → Snapshot → Take Snapshot

### 스냅샷 이름

`01-Ubuntu-Initial-Setup`

### 생성 이유

1. 정상 설치 상태를 저장한다.
2. 설정 오류가 발생하면 이전 상태로 복원할 수 있다.
3. 장애 재현 실습에 활용할 수 있다.

**주의:** 스냅샷은 별도의 안전한 백업을 대체하지 않는다.

---

## 11. 기본 장애 대응

| 장애 | 가능한 원인 | 점검 방법 |
|---|---|---|
| Ubuntu 부팅 실패 | ISO 연결·부팅 설정 문제 | VMware CD/DVD 확인 |
| VM 실행 오류 | 가상화 기능 설정 문제 | VT-x / AMD-V 확인 |
| IP 주소 없음 | NAT·DHCP 문제 | ip -br addr |
| 로그인 실패 | 계정·비밀번호 오류 | 사용자 정보 확인 |
| apt update 실패 | 인터넷·DNS 문제 | IP·라우팅·DNS 점검 |
| SSH 실행 실패 | SSH 미설치·서비스 오류 | systemctl status ssh |

### 네트워크 장애 기본 점검

```bash
ip -br addr
ip route
ping -c 4 1.1.1.1
ping -c 4 ubuntu.com
```

명령어 의미:

- `ip -br addr`: IP 주소 확인
- `ip route`: 라우팅 정보 확인
- `ping -c 4`: ICMP 테스트 패킷 4개 전송

IP 주소 통신이 가능하지만 도메인 이름으로 통신이 실패한다면 DNS 문제를 의심할 수 있다.

단, ping은 네트워크 정책에 따라 차단될 수 있으므로 실패만으로 통신 장애를 확정하지 않는다.

### 장애 대응 원칙

증상 확인 → 관련 설정 점검 → 원인 분석 → 조치 → 정상 복구 검증

---

## 12. 실무 면접 핵심 질문

### Q1. VMware에서 CPU와 RAM을 설정하는 이유는?

가상머신이 사용할 하드웨어 자원을 할당하기 위해서입니다. 서버의 예상 작업량과 호스트 자원을 고려하여 설정합니다.

### Q2. NAT와 DHCP는 무엇이 다른가요?

NAT는 네트워크 주소를 변환하는 기술이고, DHCP는 IP 주소 등의 네트워크 설정을 자동으로 할당하는 기술입니다.

### Q3. apt update와 apt upgrade의 차이는?

apt update는 최신 패키지 목록을 갱신하고, apt upgrade는 설치된 패키지를 업그레이드합니다.

### Q4. Linux 서버의 디스크 사용량은 어떻게 확인하나요?

df -h로 파일시스템 사용량을 확인하고, lsblk로 디스크와 파티션 구조를 확인합니다.

### Q5. 스냅샷을 생성하는 이유는?

정상적인 가상머신 상태를 저장해 설정 변경이나 장애 실습 이후 이전 상태로 쉽게 복원하기 위해서입니다.

---

## 13. 최종 암기 노트

| 키워드 | 핵심 |
|---|---|
| VM | 가상 컴퓨터 |
| vCPU | VM에 제공되는 가상 CPU |
| RAM | 실행 중인 프로그램의 메모리 |
| Disk | 파일과 데이터의 저장 공간 |
| ISO | OS 설치 디스크 이미지 |
| NAT | 네트워크 주소 변환 |
| DHCP | IP 설정 자동 할당 |
| Hostname | 서버 이름 |
| Username | 로그인 계정 |
| SSH | 원격 접속 서비스 |
| apt update | 패키지 목록 갱신 |
| apt upgrade | 설치된 패키지 업그레이드 |
| df -h / | 루트 파일시스템 용량 확인 |
| Snapshot | VM 상태 복구 지점 |

---

## 14. 학습 결과

- [x] VMware 가상머신 생성
- [x] CPU·RAM·Disk·NAT 설정
- [x] Ubuntu Server 24.04 LTS 설치
- [x] 사용자 및 호스트명 설정
- [x] OpenSSH Server 설치
- [x] 운영체제 정보 확인 학습
- [x] CPU·메모리·디스크 확인 학습
- [x] 패키지 업데이트 및 시간대 설정 학습
- [x] 기본 장애 대응 개념 학습
- [x] 확인문제 5/5 정답

**1장 2교시 완료 — 100점**

### 다음 학습
**1장 3교시 — Linux 네트워크·IP·DNS·라우팅·SSH 원격 접속 및 기초 장애 대응**
