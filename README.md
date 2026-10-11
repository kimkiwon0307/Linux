# 리눅스
<details>
<summary><h2>1. 기본 사용과 파일 관리</h2></summary>
   


## 리눅스 디렉터리 구조
1. /etc : 시스템/서비스 설정 파일
2. /var : 계속 변하는 데이터 로그, 캐시 등
3. /home : 일반 사용자 홈 디렉터리
4. /tmp : 임시 파일
5. /opt : 별도로 설치하는 프로그램을 두기도 함
6. /dev : 디스크, 터미널 같은 장치를 파일 형태로 표현
7. /proc : 프로세스와 커널 정보를 보여주는 가상 파일 시스템

## 절대경로와 상대경로
1. / : 절대 경로
2. 상대 경로 : 현재 위치를 기준으로
3. .. : 상위 디렉터리
4. . : 현재 디렉터리
5. ~ : 사용자의 홈 디렉터리

## 파일과 디렉터리 기본 명령
1. 현재 위치가 어디지? : pwd
2. 여기 뭐가 있지? : ls
3. 숨김 파일까지? : ls -la
4. 디렉터리 이동 : cd
5. 디렉터리 생성 : mkdir
6. 빈 파일 생성 : touch
7. 복사 : cp
8. 이동/이름 변경 : mv
9. 삭제 : rm

## 파일 내용 확인
1. 전체 내용 간단히 확인 : cat
2. 긴 파일 페이지 단위 확인 : less
3. 앞 부분 확인 : head
4. 마지막 부분 확인 : tail
5. 실시간 로그 확인: tail -f

## 파일 찾기와 내용 검색
1. 파일 자체를 찾음 : find
2. 파일 안의 문자열을 찾음 : grep

## 파이프 | 
1. 앞 명령어의 결과를 뒤 명령어의 입력으로 전달

## > 와 >>
1. 덮어 쓰기 : >
2. 뒤에 추가 : >>

## 확인 문제
📋 리눅스 1장 확인문제 정리

1. Linux에서 시스템이나 서비스 설정 파일이 주로 저장되는 디렉터리는 어디인가?
* **정답:** `/etc`

---

2. 시스템 로그가 주로 저장되는 디렉터리는 어디인가?
* **정답:** `/var/log`

---

3. 현재 작업 중인 경로를 확인하는 명령어는 무엇인가?
* **정답:** `pwd`

---

4. 숨김 파일까지 포함해서 현재 디렉터리의 파일 목록을 자세히 확인하는 명령어는 무엇인가?
* **정답:** `ls -al`

---

5. /var/log 디렉터리 아래에서 이름에 nginx가 포함된 파일을 찾는 명령어는 무엇인가?
* **정답:** `find /var/log -name "*nginx*"`

---

6. app.log 파일에서 ERROR라는 문자열이 포함된 줄만 확인하는 명령어는 무엇인가?
* **정답:** `grep "ERROR" app.log`

---

7. app.log 파일의 마지막 부분을 실시간으로 계속 확인하는 명령어는 무엇인가?
* **정답:** `tail -f app.log`

---

8. > 와 >> 의 차이는 무엇인가?
* **정답:**
  * `>` : 파일 내용을 새로 저장하거나 기존 내용을 덮어씁니다.
  * `>>` : 기존 내용을 유지하면서 파일 뒤에 내용을 추가합니다.

---

9. ps aux | grep nginx 명령에서 | 의 역할은 무엇인가?
* **정답:** 앞 명령어의 출력 결과를 뒤 명령어의 입력으로 전달합니다. (예: `ps aux`의 결과를 `grep nginx`로 넘겨서 nginx가 포함된 줄만 확인)

---

10. 현재 위치가 /home/ubuntu일 때 상위 디렉터리로 이동하는 명령어는 무엇인가?
* **정답:** `cd ..`

## 실습 1
1. 홈 디렉터리로 이동한 뒤 linux-day1 디렉터리를 생성하시오.

2. linux-day1 디렉터리 안에 app.log, config.conf, test.txt 파일을 생성하시오.

3. app.log 파일에 아래 내용을 저장하시오.

INFO server started
INFO user login
ERROR database connection failed
WARN memory usage high
ERROR timeout occurred

4. app.log에서 ERROR가 포함된 줄만 출력하시오.

5. linux-day1 디렉터리 안에서 이름에 conf가 포함된 파일을 찾으시오.

6. app.log의 마지막 2줄만 출력하시오.

7. app.log에서 ERROR가 포함된 줄만 골라 error.log 파일에 저장하시오.

8. error.log의 기존 내용을 유지하면서 아래 내용을 추가하시오.

ERROR disk full

9. config.conf 파일을 config.conf.bak이라는 이름으로 복사하시오.

10. linux-day1 디렉터리의 파일 목록을 숨김 파일까지 포함해서 자세히 확인하시오.
## 실습 2 파일 검색 + 로그 확인
1. linux-day1 디렉터리 안에서 .log로 끝나는 파일을 모두 찾으세요. find ./linux-day1 -name "*.log"
2. app.log에서 ERROR 또는 WARN이 포함된 줄만 찾으세요. grep -E "ERROR|WARN" ./linux-day1/app.log
3. app.log의 마지막 3줄만 확인하세요. tail -n 3 ./linux-day1/app.log
4. app.log에서 ERROR가 몇 줄인지 세어보세요. grep -c "ERROR" ./linux-day1/app.log
5. error.log 파일의 내용을 화면으로 확인하세요. cat ./linux-day1/error.log
6. config.conf를 config.conf.bak이라는 이름으로 복사하세요. cp ./linux-day1/config.conf ./linux-day1/config.conf.bak
7. test.txt를 /tmp로 이동하세요. mv ./linux-day1/test.txt /tmp
8. 현재 linux-day1 디렉터리의 파일 목록을 자세히 확인하세요. ls -al ./linux-day1/

## 장애 문제

1. 운영 서버에서 장애 발생, 로그 파일은 /var/log/myapp/app.log, 담당자는 방금 발생한 ERROR를 빨리 확인해 주세요. 어떤 명령어를 사용하겠습니까?
2. /var/log 아래에 로그 파일이 너무 많아서 access.log라는 파일이 어디 있는지 모르겠습니다. 어떤 명령어로 찾겠습니까?

1) tail -n 50 /var/log/myapp/app.log | grep -i "error" 또는 tail -f /var/log/myapp/app.log | grep -i "error"
2) sudo find /var/log -name "access.log"

</details>

<details>
<summary><h2>2장 사용자 그룹 권한 관리</h2></summary>

## 사용자와 그룹
1. 리눅스는 기본적으로 여러 사용자가 함께 사용하는 운영체제이다.
2. Linux 내부에서는 사용자 이름 자체보다 숫자 ID를 기준으로 사용자를 구별한다.
3. UID = User ID
4. GID = Group ID
5. id

## 왜 그룹이 필요한가?
1. 그룹으로 묶고 관리하는게 편하다.
2. 그래서 파일에는 보통 Owner, Group, Other 세 가지 기준으로 권한을 준다.

## 사용자 정보가 저장되는 곳
1. /etc/passwd : 사용자 기본 정보
2. /etc/group : 그룹 정보
3. /etc/shadow : 패스워드 관련 정보

## root와 sudo
1. root는 Linux 최고 관리자 계정이다.
2. UID = 0 이다.
3. root는 대부분의 시스템 파일을 수정하고 서비스를 제어할 수 있다.
4. 하지만 운영 서버에서 항상 root로 로그인해서 작업하면 위험하다.
5. 그래서 일반 사용자로 로그인하고 필요시에만 sudo 방식을 사용한다.
6. root : 관리자 계정 자체
7. sudo : 일반 사용자가 특정 명령을 관리자 권한으로 실행

## 파일 권한 rwx
1. r = read = 읽기 = 4
2. w = write = 쓰기 = 2
3. x = excute = 실행 = 1

## 파일과 디렉터리에서 권한 의미가 다르다.
1. 디렉터리의 x 권한이 중요하다.
2. 디럭터리에 r은 있지만 x가 없으면 목록 일부를 볼 수 있어도 내부 파일에 정상적으로 접근하기 어렵다.

## 소유권 변경
1. chown
2. sudo chown tomcat:tomcat /opt/tomcat
3. sudo chgrp 

## 사용자 생성 삭제
1. Linux에 사용자를 만들 때 대표적으로 useradd와 adduser가 있다.
2. useradd는 비교적 기본적인 저수준 명령이고, 옵션을 직접 지정해야 하는 경우가 많다.
3. adduser는 사용자 생성 과정에서 홈 디렉터리, 비밀번호 등을 비교적 편하게 설정해준다.

## 사용자 정보 변경
1. 이미 존재하는 사용자를 변경할 때는 usermod를 사용한다.
2. sudo usermod -aG developers user1
3. -a : 기존 그룹 유지하면서 추가
4. -G : 추가 그룹 지정

## 그룹 관리
1.  새 그룹 생성 : sudo groupadd developers
2.  사용자 그룹 조회 : groups user1 또는 id user1

## 서비스 전용 계정
1. sudo useradd -r -s /usr/sbin/nologin tomcat
2. -r : 시스템/서비스용 계정
3. nologin : 사람이 로그인하지 못하게 함

## sudo 권한
1. Ubuntu에서는 관리자 작업이 필요한 사용자를 sudo 그룹에 넣는 방식이 흔하다.
2. sudo usermod -aG sudo user1
3. /etc/sudoers

## sudoers와 visudo
1. /etc/sudoers는 중요한 설정 파일이다.
2. sudo visudo 는 저장 전에 문법 오류를 확인해주는 장점이 있다.

## 비밀번호 없이 sudo
1. user1 ALL=(ALL) NOPASSWD: ALL
2. user1은 sudo 사용 시 비밀번호 입력 없이 모든 명령 실행 가능

## umask
1. 새 파일을 만들 때 보통 권한을 매번 chmod 644 file 로 지정하지 않는다.
2. Linux에는 새 파일/디렉터리를 만들 때 기본 권한을 결정하는 기준이 있다.
3. 이게 umask다.
4. umask는 새로 생성되는 파일/디렉터리의 기본 권한을 제한한다.

## 확인문제
[리눅스 2장 사용자·그룹·권한 관리 확인문제 20문제]

1. UID와 GID는 각각 무엇을 의미하는가?
* **정답:** UID = User ID / GID = Group ID

---

2. root 사용자의 UID는 몇 번인가?
* **정답:** `0`

---

3. 사용자 기본 정보가 저장되는 파일은 무엇인가?
* **정답:** `/etc/passwd`

---

4. 그룹 정보가 저장되는 파일은 무엇인가?
* **정답:** `/etc/group`

---

5. 패스워드 관련 정보가 저장되는 파일은 무엇인가?
* **정답:** `/etc/shadow`

---

6. rwxr-x--- 권한을 Owner / Group / Other로 나누어 설명하시오.
* **정답:** 
  * Owner = `rwx`
  * Group = `r-x`
  * Other = `---`

---

7. r, w, x를 숫자로 나타내면 각각 몇인가?
* **정답:** `r = 4`, `w = 2`, `x = 1`

---

8. chmod 750 test.sh의 권한을 Owner / Group / Other로 설명하시오.
* **정답:** 
  * Owner = `rwx` (7)
  * Group = `r-x` (5)
  * Other = `---` (0)

---

9. 파일에서 x 권한은 무엇을 의미하는가?
* **정답:** 파일을 실행할 수 있는 권한

---

10. 디렉터리에서 x 권한은 무엇을 의미하는가?
* **정답:** 디렉터리 내부로 접근하거나, 그 안의 파일/경로에 접근할 수 있는 권한

---

11. chmod, chown, chgrp는 각각 무엇을 변경하는 명령인가?
* **정답:** 
  * `chmod` = 파일/디렉터리 권한 변경
  * `chown` = 소유자 변경
  * `chgrp` = 소유 그룹 변경

---

12. useradd와 userdel은 각각 어떤 명령인가?
* **정답:** 
  * `useradd` = 사용자 생성
  * `userdel` = 사용자 삭제

---

13. 기존 사용자를 다른 그룹에 추가하면서 기존 그룹도 유지하려면 어떤 명령 형식을 사용하는가?
* **정답:** `sudo usermod -aG 그룹명 사용자명`
  * *예시:* `sudo usermod -aG developers user1`

---

14. 사용자가 어느 그룹에 속해 있는지 확인할 수 있는 명령어 두 가지는?
* **정답:** `id user1`, `groups user1`

---

15. Tomcat 같은 서비스 계정에 nologin을 사용하는 이유는 무엇인가?
* **정답:** 서비스 실행에는 계정이 필요하지만 사람이 직접 로그인할 필요는 없기 때문에, 로그인 경로를 차단하여 보안 위험을 줄이기 위해 사용합니다.

---

16. root로 직접 작업하는 것과 일반 사용자가 sudo를 사용하는 것의 차이는 무엇인가?
* **정답:** 
  * `root`는 관리자 계정 자체이며 거의 모든 시스템 권한을 가집니다.
  * `sudo`는 일반 사용자가 허가받은 명령을 필요한 순간에 관리자 권한으로 실행하는 방식입니다.

---

17. /etc/sudoers는 어떤 파일이며 visudo를 사용하는 이유는 무엇인가?
* **정답:** 
  * `/etc/sudoers`는 누가 어떤 sudo 권한을 사용할 수 있는지 정의하는 설정 파일입니다.
  * `visudo`는 sudoers 파일을 안전하게 수정하고 저장할 때 문법 오류를 검사하기 위해 사용합니다.

---

18. NOPASSWD는 무엇이며 NOPASSWD: ALL을 무조건 사용하는 것이 좋지 않은 이유는 무엇인가?
* **정답:** 
  * `NOPASSWD`는 sudo 명령 실행 시 비밀번호 입력을 생략하도록 하는 설정입니다.
  * `NOPASSWD: ALL`은 모든 명령을 비밀번호 없이 관리자 권한으로 실행할 수 있기 때문에 계정이 탈취될 경우 위험이 큽니다. 가능한 경우 필요한 명령만 제한해서 허용하는 것이 좋습니다.

---

19. umask는 무엇을 결정하는가? umask 022일 때 일반적인 새 파일과 새 디렉터리 권한은?
* **정답:** 
  * `umask`는 새로 생성되는 파일과 디렉터리의 기본 권한을 제한합니다.
  * umask 022일 때 일반적인 권한:
    * 파일 = `644` (`rw-r--r--`)
    * 디렉터리 = `755` (`rwxr-xr-x`)

---

20. SUID, SGID, Sticky Bit, ACL을 간단히 설명하시오.
* **정답:**
  * **SUID:** 실행 파일을 실행할 때 파일 소유자의 권한으로 실행될 수 있게 하는 특수 권한
  * **SGID:** 공유 디렉터리에서 새 파일이 부모 디렉터리의 그룹을 이어받게 할 때 활용 가능한 특수 권한
  * **Sticky Bit:** 공유 디렉터리에서 다른 사용자의 파일을 함부로 삭제하지 못하도록 하는 권한 (예: `/tmp`)
  * **ACL:** 기본 Owner / Group / Other 권한만으로 부족할 때 특정 사용자나 특정 그룹에 추가로 세밀한 권한을 부여하는 기능

## 실습 문제

[리눅스 2장 기본 실습문제 8문제 + 정답]

1. user1이라는 사용자를 생성하시오.

정답:
sudo useradd user1


2. developers라는 그룹을 생성하시오.

정답:
sudo groupadd developers


3. user1 사용자를 developers 그룹에 추가하되,
기존에 속해 있던 그룹은 유지하시오.

정답:
sudo usermod -aG developers user1


4. user1 사용자가 어떤 그룹에 속해 있는지 확인하시오.

정답:
id user1

또는:
groups user1


5. /tmp/project 디렉터리를 생성하고
소유자를 user1, 소유 그룹을 developers로 변경하시오.

정답:
sudo mkdir /tmp/project
sudo chown user1:developers /tmp/project


6. /tmp/project 디렉터리의 권한을 다음과 같이 설정하시오.

Owner : rwx
Group : r-x
Other : ---

정답:
sudo chmod 750 /tmp/project


7. tomcat이라는 서비스 전용 계정을 생성하시오.
이 계정은 일반 로그인은 할 수 없도록 설정하시오.

정답:
sudo useradd -r -s /usr/sbin/nologin tomcat

확인:
getent passwd tomcat

8. 현재 사용자의 umask 값을 확인하시오.
정답:
umask


</details>












