# 🐧 Linux 

> **리눅스 명령행 인터페이스(CLI)와 셸(Shell)의 핵심 개념을 정리한 문서입니다.**

---

## 1. 명령행 인터페이스 (CLI) 핵심 정리

### 셸 (Shell)이란?
사용자가 입력한 명령어를 해석하여 **리눅스 커널(Kernel)**에게 전달하고 실행 결과를 사용자에게 보여주는 명령어 프로그램이다.

* **역할:** 사용자 ↔ 커널 사이의 다리(인터페이스) 역할
* **대표적인 셸 종류:**
    * `bash` (Bourne Again Shell): 가장 널리 쓰이는 표준 셸
    * `zsh` (Z Shell): 강력한 플러그인과 테마(Oh My Zsh)를 지원하는 최신 셸
    * `sh` (Bourne Shell): 가장 기본적인 전통 셸
* **기본 셸 확인:** Ubuntu 등 대부분의 주요 리눅스 배포판은 기본 셸로 **`bash`**를 채택하고 있습니다.

---

## 2. 시작하고 종료하기

### 📂 자주 쓰는 기본 명령어
* `pwd` : 현재 작업 중인 디렉터리 경로 출력
* `ls` : 현재 위치의 파일 및 폴더 목록 보기
* `cd` : 지정한 폴더로 이동

---

### 🌐 셸 환경변수
환경변수는 시스템이나 프로그램이 참조하는 **설정값을 저장하는 공간**입니다.

#### 📌 자주 사용하는 주요 환경변수
1. `HOME` : 현재 사용자의 홈 디렉터리 경로
2. `PATH` : 실행 파일을 찾는 명령어 검색 경로
3. `USER` : 현재 로그인한 사용자 이름
4. `HOSTNAME` : 컴퓨터(호스트)의 이름

<img width="261" height="36" alt="image" src="https://github.com/user-attachments/assets/52bfc3f0-27ac-47ac-8a35-6985f5dbd582" />
<img width="255" height="31" alt="image" src="https://github.com/user-attachments/assets/e5914995-f19a-4e72-871c-ec605bff63fc" />
<img width="803" height="38" alt="image" src="https://github.com/user-attachments/assets/5e71e07a-13fc-49b4-a521-19e8f615681f" />
<img width="285" height="39" alt="image" src="https://github.com/user-attachments/assets/ec701fc8-b8ed-4419-9cd4-1e064a006de6" />

---

### 🛑 시스템 종료 및 재부팅
* `sudo shutdown now` : 시스템 안전하게 즉시 종료
* `sudo reboot` : 시스템 재부팅
* `sudo poweroff` : 시스템 전원 즉시 차단 및 종료

---

### 👥 사용자 및 권한 관리

#### 1) 로그인 사용자 확인
* `who` : 현재 시스템에 로그인된 모든 사용자 목록 출력
* `whoami` : 현재 명령어를 실행 중인 내 계정 이름 출력

<img width="323" height="68" alt="image" src="https://github.com/user-attachments/assets/d58f5e29-8927-4b39-a83f-698d48e9cff8" />

#### 2) 루트(root) 권한 관리
루트(`root`)는 시스템의 모든 권한을 가진 최고 관리자입니다. Ubuntu 등에서는 실수를 방지하기 위해 일반 계정에서 `sudo` 명령어를 접두어로 붙여 관리자 권한을 임시로 획득합니다.

* `sudo adduser [유저네임]` : 새로운 사용자 계정 생성 (실무에서 개발자/운영 계정 분리 시 사용)
* `sudo usermod -aG sudo [유저네임]` : 특정 사용자에게 관리자(`sudo`) 권한 부여
  > ⚠️ **주의:** `-a` 옵션을 누락하면 기존에 속해 있던 다른 보조 그룹에서 강제 탈퇴되므로 반드시 `-aG` 형태로 사용해야 합니다.
* `su - [유저네임]` : 지정한 사용자의 환경변수를 적용하며 계정 전환
* `sudo su` : 최고 관리자(`root`) 계정으로 직접 전환

<img width="617" height="339" alt="image" src="https://github.com/user-attachments/assets/d2236899-416e-4fea-9af3-f0c36f83ceb1" />
<img width="288" height="82" alt="image" src="https://github.com/user-attachments/assets/939c31a8-19f6-4ba5-a35e-354a7582dfb5" />

#### 3) 그룹 관리 및 확인
리눅스는 사용자(User)와 그룹(Group)을 통해 팀별 접근 권한을 효율적으로 분리합니다.

* `getent group sudo` : `sudo` 권한을 가진 소속 사용자 목록 확인
* `grep '^sudo:' /etc/group` : 그룹 설정 파일에서 `sudo` 그룹 정보만 필터링하여 확인

<img width="414" height="51" alt="image" src="https://github.com/user-attachments/assets/a105a30c-9976-45c6-8c90-7f72d3ae9793" />

---

### 📄 파일 및 디렉터리 관리
> 💡 **리눅스의 대원칙:** "리눅스에서는 모든 것이 파일로 관리된다."

#### 1) 파일 목록 및 정보 확인
* `ls` : 파일 목록 보기
* `ls -al` : 숨김 파일을 포함한 파일 목록의 상세 정보(권한, 소유자 등) 보기

<img width="412" height="82" alt="image" src="https://github.com/user-attachments/assets/f6c87a50-c344-46b6-894e-9af5d2f34004" />

#### 2) 권한 및 소유권 변경
* **파일 권한 정보:** `r` (읽기, Read) / `w` (쓰기, Write) / `x` (실행, Execute)
* `chmod` : 파일이나 디렉터리의 접근 권한 변경
* `chown` : 파일이나 디렉터리의 소유자 및 소유 그룹 변경

<img width="435" height="96" alt="image" src="https://github.com/user-attachments/assets/028003e0-bbf1-4929-8e65-463ca383913c" />
<img width="461" height="95" alt="image" src="https://github.com/user-attachments/assets/3a67dee7-d4df-40dc-872f-8c634c9d7dd6" />

#### 3) 리눅스 주요 기본 디렉터리 구조
* `/home` : 일반 사용자들의 홈 폴더 저장 위치
* `/etc` : 시스템 및 프로그램의 환경 설정 파일 저장소
* `/var/log` : 시스템 및 애플리케이션의 로그 파일 저장소
* `/bin` : 사용자 시스템을 위한 기본 핵심 명령어 프로그램 위치
* `/usr` : 일반 사용자들이 주로 사용하는 프로그램 및 라이브러리 설치 공간
* `/tmp` : 부팅 시 혹은 주기적으로 삭제되는 임시 파일 저장소

#### 4) 디렉터리 제어
* `mkdir` : 새로운 디렉터리(폴더) 생성
* `rm -r` : 디렉터리와 그 내부 콘텐츠까지 모두 재귀적으로 삭제

<img width="519" height="20" alt="image" src="https://github.com/user-attachments/assets/acd52e7a-f887-4d61-9b40-03535d50c964" />

#### 5) 파일 제어
* `touch` : 빈 파일 생성 또는 파일의 수정 시간 업데이트
* `cp` : 파일 복사
* `mv` : 파일 이동 또는 파일 이름 변경
* `rm` : 파일 삭제

#### 6) 파일 내용 확인
* `cat` : 파일의 전체 내용 한 번에 출력
* `less` : 큰 파일 내용을 페이지 단위로 화면에 출력 (방향키 이동 가능)
* `tail -f [파일명]` : 파일의 마지막 부분을 출력하며, 추가되는 내용을 실시간 모니터링 (로그 확인용)

#### 7) 파일 및 문자열 검색
* `find / -name [파일명]` : 루트 디렉터리부터 지정한 이름의 파일 위치 검색
* `grep "[문자열]" [파일명]` : 파일 내부에서 특정 문자열이나 패턴이 포함된 라인 검색

### ⚙️ 프로세스 관리하기
> 💡 **프로세스란?** 현재 시스템에서 실행 중인 프로그램을 말합니다. 서버 장애의 대부분은 프로세스 다운(죽음), CPU 과다 사용, 메모리 부족과 관련이 깊으므로 프로세스 관리는 서버 운영의 핵심입니다.

#### 1) 프로세스 확인하기
* `ps` : 가장 기본적인 현재 프로세스 상태 출력
* `ps -ef` : 시스템에서 실행 중인 모든 프로세스를 상세히 출력
* `ps -ef | grep nginx` : 전체 프로세스 중 특정 프로세스(예: nginx)만 필터링하여 검색
* `top` : 실시간 CPU 및 메모리 사용량과 프로세스 순위 보기
* `htop` : Ubuntu 등에서 많이 사용하는 모니터링 도구로, `top`보다 시각적으로 깔끔하고 직관적임

#### 2) 열린 파일 및 포트 조회하기
* `sudo lsof -i` : 현재 네트워크(포트)를 사용 중인 모든 프로세스 표시
* `sudo lsof -i :80` : 현재 80번 포트(웹 서비스 등)를 어떤 프로세스가 점유하고 있는지 확인

#### 3) 작업 제어하기
리눅스는 명령어를 눈앞에서 실행하는 **포그라운드(Foreground)**와 뒤에서 조용히 실행하는 **백그라운드(Background)** 개념이 있습니다.

* `[명령어] &` : 명령어를 백그라운드에서 실행 (예: `sleep 100 &`을 입력하면 100초 대기 작업을 뒤로 던져 터미널을 계속 사용할 수 있음)
* `jobs` : 현재 백그라운드에서 실행 중인 작업 목록 표시
* `fg` : 백그라운드에서 돌고 있는 작업을 다시 눈앞(Foreground)으로 가져오기

<img width="1202" height="535" alt="image" src="https://github.com/user-attachments/assets/1614bada-03d1-428a-98e3-27b3f28625c6" />

#### 4) 프로세스 상태 변경하기
* `kill [PID]` : 지정한 프로세스 ID(PID)에 종료 신호를 보내 안전하게 종료
* `kill -9 [PID]` : 프로세스를 예외 없이 즉시 강제 종료 (안전한 종료가 안 될 때 최종 수단으로 사용)
* `pkill nginx` : PID를 모를 때, 프로세스의 이름(예: nginx)을 지정하여 일괄 종료

---

### 📦 패키지 관리하기
> 💡 **패키지란?** 리눅스 프로그램의 설치 파일 묶음입니다. (윈도우의 `.exe` 설치 파일과 유사합니다.)

#### 1) dpkg (데비안 패키지 관리 도구)
Ubuntu는 데비안(Debian) 계열 리눅스이기 때문에 `.deb` 확장자의 패키지 파일을 사용합니다.
* `sudo dpkg -i file.deb` : 다운로드한 패키지 파일 설치
* `dpkg -l` : 시스템에 설치된 전체 패키지 목록 확인
> 🛠️ *참고:* 의존성(함께 설치되어야 하는 파일들)을 스스로 해결하지 못하므로, 실무에서는 주로 아래의 `apt`를 사용합니다.

#### 2) apt (고급 패키지 도구)
인터넷 저장소에서 패키지와 의존성 파일까지 알아서 다운로드해 설치해 주는 Ubuntu의 핵심 패키지 관리자입니다.
* `sudo apt update` : 인터넷 저장소의 최신 패키지 목록(인덱스) 업데이트 (설치 전 필수 실행)
* `sudo apt upgrade` : 현재 설치된 모든 패키지를 최신 버전으로 업그레이드
* `sudo apt install nginx` : 특정 패키지(예: nginx) 설치
* `sudo apt remove nginx` : 설치된 패키지 삭제
* `apt search nginx` : 원하는 패키지가 저장소에 있는지 이름으로 검색

---

### 🛠️ 서비스 관리하기
> 💡 **서비스(Service)란?** 사용자가 로그인하지 않아도 시스템 백그라운에서 지속적으로 실행되는 프로그램입니다. (예: nginx, ssh, mysql, docker 등)

#### 1) systemd 개요
* Ubuntu의 기본 시스템 관리자입니다.
* 서비스의 시작/중지, 부팅 시 자동 실행, 로그 관리, 시스템 상태 관리가 주요 역할입니다.

#### 2) systemctl 상태 조회
서버 장애 발생 시 서비스가 살아있는지 확인하는 것이 가장 첫 단계이므로 매우 중요합니다.
* `systemctl status nginx` : 특정 서비스(예: nginx)의 현재 상태 보기
* `systemctl list-units --type=service` : 시스템에 등록된 전체 서비스 목록 확인

#### 3) 서비스 제어
실무에서 소스 배포나 설정 변경을 진행한 후 서비스를 재시작하는 흐름이 가장 중요하게 사용됩니다.
* `sudo systemctl start nginx` : 서비스 시작
* `sudo systemctl stop nginx` : 서비스 중지
* `sudo systemctl restart nginx` : 서비스 재시작 (**★배포 후 설정 적용 시 가장 중요**)
* `sudo systemctl enable nginx` : 시스템이 부팅될 때 자동으로 서비스가 실행되도록 등록
* `sudo systemctl disable nginx` : 부팅 시 자동 실행 해제

#### 4) journalctl 로그 조회
`systemd` 기반 시스템 환경에서 발생하는 로그를 확인하는 전용 도구입니다.
* `journalctl` : 시스템의 전체 로그 확인
* `journalctl -u nginx` : 특정 서비스(예: nginx)와 관련된 로그만 필터링하여 확인
* `journalctl -f` : 로그의 마지막 부분을 실시간으로 모니터링 (오류 디버깅 및 장애 확인용)

---

### 📝 vi/vim 편집기 익히기
우분투 및 리눅스 환경에서 텍스트 기반 파일을 수정할 때 가장 범용적으로 사용하는 편집기입니다. (우분투에서는 기능이 향상된 `vim`을 주로 사용합니다.)

#### 1) vi의 3가지 핵심 모드
* **명령 모드 :** 파일 실행 시 최초 상태. 커서 이동, 삭제, 복사 등이 가능합니다.
* **입력 모드 :** 실제 글자를 입력할 수 있는 상태입니다.
* **ex 모드 :** 저장, 종료, 검색 등을 수행하는 모드입니다. (명령 모드에서 `:` 입력 시 진입)

#### 2) 핵심 단축키 요약 (명령 모드 기준)
* `i` : 현재 커서 위치에서 **입력 모드**로 진입
* `ESC` : 입력 모드나 ex 모드에서 다시 **명령 모드**로 복귀
* `dd` : 커서가 위치한 **한 줄 삭제**
* `yy` : 커서가 위치한 **한 줄 복사**
* `p` : 복사하거나 삭제한 한 줄을 커서 아래에 **붙여넣기**
* `u` : 직전에 실행한 작업 **실행 취소** (Undo)

#### 3) 파일 작성 및 관리 프로세스
* `vim test.txt` : `test.txt` 파일을 열거나, 없는 경우 새로 생성하면서 편집기 실행
* 입력 모드(`i`)로 전환 후 내용 작성 -> 작성 완료 후 `ESC`를 눌러 명령 모드로 복귀 -> `:`를 눌러 ex 모드로 전환 후 저장/종료 명령 입력

#### 4) 주요 ex 모드 명령 종류
* `:w` : 작업 내용 저장
* `:q` : 변경 사항이 없을 때 편집기 종료
* `:wq` : **작업 내용 저장 후 완전히 종료**
* `:q!` : 변경 사항을 저장하지 않고 **강제 종료**





