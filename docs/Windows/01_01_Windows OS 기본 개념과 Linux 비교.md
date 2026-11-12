
# Windows OS 프로젝트식 학습
## 1장 1교시 — Windows OS 기본 개념과 Linux 비교

### 1. 운영체제(OS)란?

OS(Operating System)는 컴퓨터의 하드웨어 자원을 관리하고 사용자와 응용 프로그램이 컴퓨터를 사용할 수 있도록 지원하는 소프트웨어이다.

**운영체제의 주요 역할**

| 역할 | 설명 |
|---|---|
| CPU 관리 | 프로세스 실행 순서와 CPU 사용 시간 관리 |
| 메모리 관리 | 프로그램에 메모리 할당 및 보호 |
| 프로세스 관리 | 프로그램 실행, 종료, 상태 관리 |
| 파일 관리 | 파일 저장, 읽기, 삭제 및 권한 관리 |
| 장치 관리 | 디스크, 네트워크 카드 등 하드웨어 제어 |
| 보안 관리 | 사용자 인증 및 접근 권한 통제 |

**기본 구조**

사용자 → 응용 프로그램 → 운영체제 → 하드웨어

예시:
- 사용자가 Chrome 실행
- Windows가 Chrome 프로세스 생성
- CPU와 메모리 자원 할당
- 필요한 파일 및 네트워크 접근 처리

---

### 2. Windows OS란?

Windows는 Microsoft에서 개발한 운영체제이다.

**Windows 주요 종류**

| 구분 | Windows 11 | Windows Server |
|---|---|---|
| 용도 | 개인 및 업무용 PC | 기업 서버 운영 |
| 주요 기능 | 일반 프로그램 실행 | 인증, 파일, DNS, 웹 서비스 |
| 관리 도구 | 설정, 작업 관리자 | Server Manager, PowerShell |
| 주요 특징 | 사용자 편의성 중심 | 서버 역할 및 중앙 관리 기능 제공 |

**Windows Server의 주요 역할**
- Active Directory: 사용자 계정 및 인증 관리
- DNS Server: 도메인 이름을 IP 주소로 변환
- DHCP Server: IP 주소 자동 할당
- File Server: 파일 공유 및 권한 관리
- IIS: 웹 서버 운영

---

### 3. Windows 내부 구조

Windows는 Windows NT 커널 기반 운영체제이다.

주요 실행 영역은 User Mode와 Kernel Mode로 나뉜다.

#### ① User Mode (사용자 모드)

일반 응용 프로그램이 주로 실행되는 영역이다.

예시:
- Chrome
- 메모장
- PowerShell

특징:
- 일반 응용 프로그램 실행
- 보호된 커널 메모리에 직접 접근 불가
- 운영체제가 제공하는 인터페이스를 통해 시스템 기능 요청

#### ② Kernel Mode (커널 모드)

운영체제의 핵심 기능과 많은 장치 드라이버가 실행되는 영역이다.

주요 역할:
- 프로세스 스케줄링
- 메모리 관리
- 장치 및 I/O 처리
- 시스템 자원 관리

**핵심 차이**

User Mode는 일반 프로그램을 실행하는 보호된 영역이며, Kernel Mode는 운영체제 핵심 기능을 수행하는 높은 권한의 영역이다.

---

### 4. Process와 Service

#### ① Process (프로세스)

실행 중인 프로그램의 인스턴스이다.

특징:
- 프로세스마다 PID(Process ID)가 부여됨
- CPU와 메모리 등의 자원을 사용함
- 실행 및 종료 상태를 가짐

예시:
- chrome.exe
- notepad.exe
- powershell.exe

#### ② Service (서비스)

Windows에서 운영체제가 관리하는 서비스 프로그램이다.

특징:
- 사용자 로그인 없이도 실행 가능
- 자동, 수동, 사용 안 함 등의 시작 유형 존재
- 백그라운드에서 시스템 기능 제공 가능

대표적인 서비스:
- Windows Event Log: 이벤트 로그 관리
- Windows Update: 업데이트 관리
- DNS Client: DNS 관련 기능
- Windows Time: 시간 동기화

**Process와 Service의 차이**

- Process: 실행 중인 프로그램
- Service: Windows 서비스 관리 체계에서 관리되는 프로그램
- 하나의 프로세스가 여러 서비스를 실행할 수도 있음

---

### 5. Windows와 Linux 비교

| 구분 | Windows | Linux |
|---|---|---|
| 커널 | Windows NT | Linux Kernel |
| GUI | 일반 데스크톱에 기본 제공 | 선택 가능 |
| CLI | CMD, PowerShell | Bash 등 |
| 파일 시스템 | NTFS | ext4, XFS 등 |
| 사용자 경로 | C:\Users\ | /home/ |
| 서비스 관리 | services.msc, Get-Service | systemctl |
| 프로세스 관리 | 작업 관리자, Get-Process | ps, top |
| 로그 관리 | 이벤트 뷰어 | journalctl |
| 웹 서버 | IIS, Apache, Nginx 등 | Apache, Nginx 등 |

**중요**

Windows와 Linux 모두 GUI와 CLI를 지원하며, 프로세스·메모리·파일·네트워크를 관리하는 기본적인 OS 원리는 같다.

---

### 6. Windows PowerShell 기본 명령어

#### ① 운영체제 정보 확인

```powershell
Get-CimInstance Win32_OperatingSystem |
    Select-Object Caption, Version, OSArchitecture
```

- Get-CimInstance: 시스템 관리 정보 조회
- Win32_OperatingSystem: 운영체제 정보 클래스
- Select-Object: 필요한 속성 선택
- Caption: OS 이름
- Version: 내부 버전
- OSArchitecture: OS 아키텍처

#### ② 프로세스 확인

```powershell
Get-Process
```

프로세스 5개만 확인:

```powershell
Get-Process | Select-Object -First 5
```

- Get-Process: 실행 중인 프로세스 조회
- -First 5: 처음 5개만 출력

#### ③ Windows 서비스 확인

```powershell
Get-Service
```

특정 서비스 확인:

```powershell
Get-Service -Name EventLog
```

상태 의미:
- Running: 실행 중
- Stopped: 중지 상태

※ Stopped가 반드시 장애를 의미하지는 않는다.

#### ④ GUI 관리 도구

| 실행 방법 | 관리 기능 |
|---|---|
| Ctrl + Shift + Esc | 작업 관리자 |
| services.msc | 서비스 관리 |
| eventvwr.msc | 이벤트 뷰어 |
| msinfo32 | 시스템 정보 |
| taskschd.msc | 작업 스케줄러 |

---

### 7. Windows와 Linux 명령어 비교

| 목적 | Windows PowerShell | Linux |
|---|---|---|
| 프로세스 확인 | Get-Process | ps aux |
| 서비스 상태 확인 | Get-Service | systemctl status |
| 서비스 시작 | Start-Service | systemctl start |
| 서비스 중지 | Stop-Service | systemctl stop |
| IP 확인 | ipconfig | ip addr |
| 연결 확인 | ping | ping |
| 로그 확인 | Get-WinEvent | journalctl |

※ 서비스 관리 명령어는 대상 서비스와 운영체제에 따라 관리자 권한이 필요할 수 있다.

---

### 8. 실무 장애 대응

**상황: Windows 서버에서 프로그램이 응답하지 않는 경우**

1. 작업 관리자 또는 Get-Process로 프로세스 확인
2. Get-Service로 관련 서비스 실행 상태 확인
3. CPU, 메모리, 디스크 사용률 확인
4. 이벤트 뷰어에서 오류 로그 확인
5. 원인 분석 후 필요한 조치 수행
6. 프로그램 또는 서비스 정상 동작 재검증

**핵심 장애 대응 순서**

상태 확인 → 로그 확인 → 원인 분석 → 조치 → 재검증

운영체제가 달라도 장애 대응의 기본적인 절차는 동일하다.

---

### 9. 핵심 개념 암기

| 개념 | 핵심 내용 |
|---|---|
| OS | 하드웨어 자원과 프로그램 실행을 관리 |
| Kernel | 운영체제의 핵심 기능 담당 |
| User Mode | 일반 응용 프로그램이 주로 실행되는 영역 |
| Kernel Mode | 핵심 OS 기능과 많은 드라이버가 실행되는 영역 |
| Process | 실행 중인 프로그램 인스턴스 |
| PID | 프로세스를 식별하는 번호 |
| Service | Windows가 관리하는 서비스 프로그램 |
| PowerShell | Windows 시스템 관리 및 자동화 도구 |
| Windows Server | 기업의 서버 역할과 중앙 관리 기능 제공 |

---

### 10. 기술면접 예상 질문

**Q1. 운영체제(OS)란 무엇인가요?**

운영체제는 CPU, 메모리, 디스크 등의 하드웨어 자원을 관리하고 응용 프로그램이 실행될 수 있도록 지원하는 소프트웨어입니다.

**Q2. 프로세스와 서비스의 차이는 무엇인가요?**

프로세스는 실행 중인 프로그램의 인스턴스이며, 서비스는 운영체제의 서비스 관리 체계에서 관리되는 프로그램입니다.

**Q3. User Mode와 Kernel Mode의 차이는 무엇인가요?**

User Mode는 일반 응용 프로그램이 주로 실행되는 보호된 영역이고, Kernel Mode는 운영체제 핵심 기능과 장치 드라이버 등이 높은 권한으로 실행되는 영역입니다.

**Q4. Windows와 Linux의 차이는 무엇인가요?**

Windows는 Windows NT 커널을 사용하고 Linux는 Linux 커널을 사용합니다. 두 운영체제 모두 GUI와 CLI를 지원하지만, 시스템 설정 및 서비스 관리 방식과 사용하는 도구에 차이가 있습니다.

**Q5. Windows 서버에서 서비스 장애가 발생하면 어떻게 대응하나요?**

먼저 서비스와 관련 프로세스 상태를 확인하고 CPU·메모리 사용률과 이벤트 로그를 분석합니다. 이후 원인에 맞게 조치하고 정상 동작 여부를 검증하겠습니다.

---

### 11. 1장 1교시 최종 요약

1. OS는 컴퓨터의 하드웨어 자원을 관리한다.
2. Windows는 Windows NT 커널 기반 운영체제이다.
3. User Mode와 Kernel Mode는 권한과 보호 수준이 다르다.
4. Process는 실행 중인 프로그램이며 Service는 Windows가 관리하는 서비스 프로그램이다.
5. Windows와 Linux는 내부 구현과 관리 도구가 다르지만 기본 운영 원리는 유사하다.
6. Windows 관리에는 작업 관리자, 서비스 관리 도구, PowerShell 등을 사용한다.
7. 장애 발생 시 상태와 로그를 확인하고 원인을 분석한 뒤 조치한다.

**학습 완료: 1장 1교시 — Windows OS 기본 개념**

<img width="1214" height="1295" alt="image" src="https://github.com/user-attachments/assets/15126ebc-fcf9-40b8-b8cd-7be2478b1cd4" />


