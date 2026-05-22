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









