
<img width="1055" height="1491" alt="image" src="https://github.com/user-attachments/assets/24a14bed-293c-494f-8988-e5a504e2fed5" />


# Linux 프로젝트 — 1장 3교시
## Linux 네트워크 구성 및 SSH 원격 접속·장애 대응

- 학습 과정: Linux 프로젝트 14장 18교시
- 실습 환경: VMware Workstation + Ubuntu Server 24.04 LTS
- 실습 서버: linux01
- 학습 주제: IP, Subnet, Gateway, DNS, DHCP, NAT, SSH

---

## 1. IP 주소란?

IP 주소는 네트워크에서 장치를 식별하고 데이터를 전달하는 데 사용하는 논리적인 주소이다.

예시:

```text
IP Address : 192.168.10.50
Subnet Mask: 255.255.255.0
CIDR       : 192.168.10.50/24
```

- IP 주소: 장치를 식별하는 논리적 주소
- Subnet Mask: 네트워크 부분과 호스트 부분 구분
- CIDR /24: 앞 24비트가 네트워크 부분

위 IP가 속한 네트워크는 `192.168.10.0/24`이다.

---

## 2. Subnet(서브넷)

Subnet은 IP 네트워크를 논리적으로 나눈 구역이다.

### 필요한 이유
- IP 주소를 체계적으로 관리
- 네트워크를 목적별로 분리
- 네트워크 간 통신 및 보안 정책 관리

예시:

```text
192.168.10.0/24 → WEB 서버 네트워크
192.168.20.0/24 → WAS 서버 네트워크
192.168.30.0/24 → DB 서버 네트워크
```

서로 다른 서브넷 간 통신에는 일반적으로 라우팅이 필요하다.

---

## 3. Gateway(게이트웨이)

Gateway는 다른 네트워크로 통신할 때 패킷을 전달하는 라우터이다.

예시:

```text
Linux 서버: 192.168.10.50
Gateway   : 192.168.10.1
```

다른 네트워크로 통신할 때 사용할 수 있는 기본 경로를 Default Route라고 한다.

```bash
ip route
```

출력 예시:

```text
default via 192.168.10.1 dev ens33
```

- `default`: 기본 경로
- `via`: 다음으로 전달할 게이트웨이
- `dev ens33`: 사용하는 네트워크 인터페이스

**핵심:** 목적지까지의 더 구체적인 경로가 없으면 기본 경로를 사용한다.

---

## 4. DNS (Domain Name System)

DNS는 도메인 이름을 IP 주소 등으로 해석하는 시스템이다.

예시:

```text
ubuntu.com → DNS 조회 → IP 주소
```

### DNS가 필요한 이유

사람은 IP 주소보다 도메인 이름을 기억하기 쉽기 때문이다.

### DNS 점검 명령어

```bash
resolvectl status
getent ahostsv4 ubuntu.com
```

- `resolvectl status`: 현재 DNS 설정 확인
- `getent ahostsv4`: 시스템 이름 해석을 통해 IPv4 주소 조회

IP 주소로 통신이 가능하지만 도메인 이름 해석이 실패한다면 DNS 문제를 의심할 수 있다.

---

## 5. DHCP와 Static IP

### DHCP

DHCP는 클라이언트에 네트워크 설정을 자동으로 제공하는 프로토콜이다.

제공 가능한 정보:
- IP 주소
- 서브넷 마스크
- 기본 게이트웨이
- DNS 서버

### Static IP

관리자가 직접 설정한 고정 IP 주소이다.

| 구분 | DHCP | Static IP |
|---|---|---|
| IP 할당 | 자동 | 수동 |
| 주소 변경 | 변경 가능 | 설정 유지 시 고정 |
| 관리 | 편리함 | 직접 관리 필요 |
| 활용 | 일반 PC·실습 | 고정 주소가 필요한 서버 |

이번 프로젝트에서는 VMware NAT의 DHCP를 사용한다.

---

## 6. NAT (Network Address Translation)

NAT는 네트워크 주소를 변환하는 기술이다.

VMware NAT 환경에서는 가상머신이 가상 네트워크를 통해 외부와 통신할 때 주소 변환을 사용한다.

### 기본 구조

```text
Ubuntu VM (linux01)
        |
        ↓
VMware 가상 네트워크
        |
        ↓
VMware NAT
        |
        ↓
외부 네트워크
```

### NAT와 DHCP의 차이

- NAT: 네트워크 주소 변환
- DHCP: IP 주소 등 네트워크 설정 자동 할당

두 기능은 역할이 다르다.

---

## 7. Linux 네트워크 확인 명령어

### 7-1. IP 주소 확인

```bash
ip -br -4 addr
```

옵션 설명:

- `ip`: 네트워크 설정·상태 관리 도구
- `-br`: 간단한 형식으로 출력
- `-4`: IPv4 정보 표시
- `addr`: IP 주소 정보

출력 예시:

```text
lo      UNKNOWN  127.0.0.1/8
ens33   UP       192.168.111.130/24
```

- `lo`: Loopback 인터페이스
- `127.0.0.1`: 자기 자신을 가리키는 주소
- `ens33`: 네트워크 인터페이스 이름 예시
- `UP`: 인터페이스 활성화

※ IP 주소와 인터페이스 이름은 환경마다 다르다.

### 7-2. 라우팅 확인

```bash
ip route
ip route get 1.1.1.1
```

- `ip route`: 라우팅 테이블 확인
- `ip route get`: 특정 목적지로 통신할 때 선택되는 경로 확인

### 7-3. DNS 확인

```bash
resolvectl status
getent ahostsv4 ubuntu.com
```

### 7-4. 네트워크 통신 확인

```bash
ping -c 4 1.1.1.1
```

- `ping`: ICMP Echo 요청을 이용한 통신 확인
- `-c 4`: 요청 패킷 4개 전송

※ ICMP가 차단된 환경에서는 ping 실패만으로 전체 네트워크 장애를 확정할 수 없다.

---

## 8. Netplan

Netplan은 Ubuntu에서 네트워크 설정을 정의하는 도구이다.

네트워크 설정 파일은 일반적으로 `/etc/netplan/` 디렉터리에 위치한다.

DHCP 설정 예시:

```yaml
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: true
```

설정 의미:

- `network`: 네트워크 설정
- `version: 2`: Netplan 설정 형식
- `ethernets`: 이더넷 인터페이스 설정
- `ens33`: 네트워크 인터페이스 이름
- `dhcp4: true`: IPv4 주소를 DHCP로 설정

현재 설정 확인:

```bash
sudo netplan get
```

※ 이 교시에서는 DHCP 설정을 유지하고, 고정 IP 및 상세 라우팅 변경은 6장에서 실습한다.

---

## 9. SSH (Secure Shell)

SSH는 네트워크를 통해 원격 서버에 암호화된 연결로 접속하는 프로토콜이다.

### SSH가 필요한 이유

- 서버에 직접 모니터와 키보드를 연결하지 않고 관리
- 원격 명령어 실행
- 암호화된 통신 제공
- 사용자 인증 및 서버 인증

### SSH 주요 용어

| 용어 | 의미 |
|---|---|
| SSH Client | 원격 접속 요청 프로그램 |
| SSH Server | 원격 접속을 받아 처리하는 프로그램 |
| sshd | SSH 서버 데몬 |
| ssh | SSH 클라이언트 명령어 |
| TCP 22 | SSH 기본 포트 |

### SSH 연결 구조

```text
Windows PC
SSH Client
     |
     | TCP 22 / 암호화 통신
     ↓
Linux01
SSH Server (sshd)
     |
     ↓
Ubuntu Shell
```

---

## 10. OpenSSH Server 설치 및 운영

### 설치 및 실행

```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl enable --now ssh
```

명령어 설명:

- `apt update`: 패키지 목록 갱신
- `apt install`: 패키지 설치
- `systemctl`: systemd 서비스 관리
- `enable`: 부팅 시 자동 시작 등록
- `--now`: 즉시 서비스 시작

### SSH 서비스 상태 확인

```bash
systemctl is-active ssh
systemctl is-enabled ssh
```

정상 실행 예시:

```text
active
enabled
```

### SSH 포트 확인

```bash
sudo ss -lntp | grep ':22'
```

옵션 설명:

- `-l`: Listen 상태
- `-n`: 주소·포트를 숫자로 표시
- `-t`: TCP 소켓
- `-p`: 프로세스 정보
- `grep ':22'`: 22번 포트가 포함된 줄 검색

### UFW 방화벽 확인

```bash
sudo ufw status
```

UFW 활성 상태에서 SSH가 허용되지 않은 경우:

```bash
sudo ufw allow 22/tcp
```

`22/tcp`는 SSH의 기본 TCP 포트를 의미한다.

---

## 11. Windows에서 SSH 접속하기

Ubuntu에서 IP를 확인한다.

```bash
ip -br -4 addr
```

Windows PowerShell에서 접속:

```powershell
# 실제 linux01 IP로 변경
ssh infra@192.168.111.130
```

위 IP 주소는 예시이다.

MobaXterm을 사용할 경우:

| 설정 | 값 |
|---|---|
| Session | SSH |
| Remote Host | linux01 실제 IP |
| Username | infra |
| Port | 22 |

### 접속 성공 검증

```bash
whoami
hostname
pwd
```

예상 결과:

```text
infra
linux01
/home/infra
```

접속 종료:

```bash
exit
```

`exit`는 원격 Shell 세션을 종료하는 명령어이며 서버 자체를 종료하지 않는다.

---

## 12. SSH 장애 대응

### 자주 발생하는 오류

| 증상 | 의심 원인 |
|---|---|
| Connection timed out | 네트워크·방화벽·경로 문제 |
| Connection refused | SSH 서비스 중지·포트 미수신 등 |
| Permission denied | 사용자 인증 실패 |
| Could not resolve hostname | DNS 또는 이름 해석 오류 |
| Host key changed | 서버 호스트 키 변경 또는 보안 문제 |

### SSH 장애 분석 명령어

```bash
systemctl status ssh --no-pager
sudo ss -lntp | grep ':22'
sudo journalctl -u ssh -n 20 --no-pager
```

명령어 설명:

- `systemctl status ssh`: SSH 서비스 상태 확인
- `ss -lntp`: TCP Listen 소켓 확인
- `journalctl -u ssh`: SSH 서비스 로그 확인
- `-n 20`: 최근 로그 20줄 출력
- `--no-pager`: 페이지 출력 프로그램을 사용하지 않음

### SSH 서비스 복구

```bash
sudo systemctl start ssh
systemctl is-active ssh
```

복구 후 Windows에서 다시 SSH로 접속하여 정상 여부를 확인한다.

※ 장애 실습은 VMware 콘솔로 직접 로그인할 수 있을 때만 수행한다.

※ Ubuntu 환경에서 SSH 소켓 활성화가 사용되는 경우 서비스 중지만으로 신규 접속이 차단되지 않을 수도 있다. 따라서 실제 포트 상태까지 검증한다.

### 장애 대응 순서

```text
SSH 접속 실패
      ↓
서버 IP 주소 확인
      ↓
네트워크 경로 확인
      ↓
TCP 22 포트 확인
      ↓
SSH 서비스 상태·로그 분석
      ↓
원인에 맞는 조치
      ↓
SSH 재접속 및 정상 검증
```

---

## 13. 면접 예상 질문

### Q1. IP 주소와 서브넷의 차이는?

IP 주소는 네트워크의 장치를 식별하는 논리적 주소이며, 서브넷은 IP 네트워크를 논리적으로 나눈 구역입니다.

### Q2. 기본 게이트웨이란?

목적지까지 더 구체적인 경로가 없을 때 패킷을 전달하는 데 사용하는 기본 경로상의 다음 홉 라우터입니다.

### Q3. NAT와 DHCP의 차이는?

NAT는 네트워크 주소를 변환하고, DHCP는 IP 주소 등의 네트워크 설정을 자동으로 제공하는 프로토콜입니다.

### Q4. SSH를 사용하는 이유는?

원격 서버에 암호화된 연결로 접속하여 안전하게 서버를 관리하기 위해서입니다.

### Q5. SSH 접속이 안 된다면?

IP·라우팅·포트 22·방화벽·SSH 서비스·인증 상태를 순서대로 점검하고, 로그를 통해 원인을 분석한 후 복구합니다.

---

## 14. 최종 암기 노트

| 키워드 | 핵심 개념 |
|---|---|
| IP | 네트워크 장치의 논리적 주소 |
| Subnet | 네트워크를 나눈 논리적 구역 |
| Gateway | 다른 네트워크로 패킷 전달 |
| Default Route | 더 구체적인 경로가 없을 때 사용하는 경로 |
| DNS | 도메인 이름 해석 |
| DHCP | 네트워크 설정 자동 할당 |
| NAT | 네트워크 주소 변환 |
| Netplan | Ubuntu 네트워크 설정 도구 |
| SSH | 암호화된 원격 접속 |
| TCP 22 | SSH 기본 포트 |
| systemctl | systemd 서비스 관리 |
| journalctl | systemd 저널 로그 확인 |
| ss | 네트워크 소켓 상태 확인 |
| ip route | 라우팅 테이블 확인 |

---

## 15. 학습 완료 체크리스트

- [ ] IP·Subnet·Gateway·DNS 개념 이해
- [ ] DHCP와 NAT의 차이 이해
- [ ] Linux IP 주소 확인
- [ ] 라우팅 및 DNS 확인
- [ ] OpenSSH Server 설치 및 서비스 확인
- [ ] Windows에서 SSH 원격 접속 성공
- [ ] SSH 접속 장애 분석 및 복구
- [ ] 객관식 확인문제 완료

### 다음 학습

**2장 1교시 — Linux 파일·디렉터리 구조 및 기본 명령어**
