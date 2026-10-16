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

## 실무형 권한 문제
[리눅스 2장 실무형 권한 실습 5문제 + 정답]


1. /data/share 디렉터리를 생성하고,
소유자는 user1,
소유 그룹은 developers로 설정하시오.

권한:
Owner = rwx
Group = rwx
Other = ---

정답:

sudo mkdir -p /data/share
sudo chown user1:developers /data/share
sudo chmod 770 /data/share

확인:
ls -ld /data/share

설명:
770
Owner = rwx = 7
Group = rwx = 7
Other = --- = 0


2. user2 사용자를 생성하고 developers 그룹에 추가하시오.
그 후 user2가 /data/share에 접근 가능한지 확인하시오.

정답:

sudo useradd user2
sudo usermod -aG developers user2

그룹 확인:
id user2

접근 확인:
sudo -u user2 ls /data/share

또는:
sudo -u user2 test -x /data/share && echo "접근 가능"

설명:
user2가 developers 그룹에 속해 있고,
/data/share의 그룹이 developers이며
그룹에 rwx 권한이 있으므로 접근할 수 있다.


3. /data/app 디렉터리를 생성하고
소유자와 소유 그룹을 tomcat으로 설정하시오.

tomcat만 모든 권한을 가지며
다른 사용자는 접근할 수 없도록 설정하시오.

정답:

sudo mkdir -p /data/app
sudo chown tomcat:tomcat /data/app
sudo chmod 700 /data/app

확인:
ls -ld /data/app

설명:
700
Owner = rwx
Group = ---
Other = ---

따라서 tomcat만 접근할 수 있다.


4. /data/shared를 developers 그룹이 공동으로 사용한다.

그 안에서 새 파일을 만들었을 때
부모 디렉터리의 developers 그룹을 상속하도록 설정하시오.

정답:

sudo mkdir -p /data/shared
sudo chown root:developers /data/shared
sudo chmod 2770 /data/shared

확인:
ls -ld /data/shared

설명:
앞의 2가 SGID이다.

2770
2    = SGID
7    = Owner rwx
7    = Group rwx
0    = Other ---

SGID가 설정된 디렉터리 안에서 파일을 만들면
새 파일이 부모 디렉터리의 그룹인 developers를 상속받는다.

ls -ld에서 예:

drwxrws--- ...

처럼 Group 실행 위치에 s가 표시될 수 있다.


5. /tmp/test-share에서 모든 사용자가 파일을 만들 수 있지만
다른 사용자가 만든 파일을 함부로 삭제하지 못하도록 설정하시오.

정답:

sudo mkdir -p /tmp/test-share
sudo chmod 1777 /tmp/test-share

확인:
ls -ld /tmp/test-share

설명:
앞의 1이 Sticky Bit이다.

1777
1    = Sticky Bit
7    = Owner rwx
7    = Group rwx
7    = Other rwx

모든 사용자가 디렉터리를 사용할 수 있지만
일반적으로 자신이 소유하지 않은 파일을 함부로 삭제할 수 없다.

ls -ld에서 예:

drwxrwxrwt ...

처럼 마지막에 t가 표시된다.

/tmp 디렉터리가 대표적인 예이다.

## 권한 관련 장애 대응 문제
[리눅스 2장 장애 대응 4문제]

1. user2 사용자가 /data/project 디렉터리에 들어가려고 했는데
"Permission denied"가 발생했다.

확인해보니:

drwxr----- 2 user1 developers /data/project

user2는 developers 그룹에 속해 있다.

문제 원인은 무엇이며 어떻게 해결할 수 있는가?

정답:
디렉터리에 Group의 x 권한이 없기 때문이다.

현재 Group 권한은 r-- 이므로
디렉터리 목록 관련 권한은 있어도 내부 접근이 불가능하다.

해결 예:
sudo chmod 750 /data/project

또는 그룹에 쓰기까지 필요하면:
sudo chmod 770 /data/project


2. Tomcat 서비스가 시작되지 않는다.

로그를 확인해보니:
/data/tomcat 디렉터리에 접근할 수 없다는 메시지가 나온다.

확인 결과:

drwx------ root root /data/tomcat

Tomcat은 tomcat 계정으로 실행된다.

원인과 해결 방법은?

정답:
tomcat 계정이 /data/tomcat 디렉터리에 접근할 권한이 없기 때문이다.

소유자를 tomcat으로 변경할 수 있다.

sudo chown -R tomcat:tomcat /data/tomcat

필요한 권한도 확인한다.

예:
sudo chmod 750 /data/tomcat

핵심:
서비스가 어떤 사용자로 실행되는지와
파일/디렉터리 소유권 및 권한을 함께 확인해야 한다.


3. user1을 developers 그룹에 추가했다.

sudo usermod -aG developers user1

그런데 현재 로그인된 user1 세션에서
developers 그룹 권한이 바로 적용되지 않는다.

왜 그런가?

정답:
현재 로그인 세션은 그룹 정보 변경 전에 만들어진 세션이기 때문이다.

로그아웃 후 다시 로그인하면 새 그룹 정보가 적용된다.

확인:
id user1

또는 새 세션에서:
groups


4. 일반 사용자가 다음 명령을 실행했다.

sudo systemctl restart nginx

하지만
"user is not in the sudoers file"
또는 sudo 권한이 없다는 오류가 발생했다.

원인과 해결 방법은?

정답:
해당 사용자에게 sudo 권한이 없기 때문이다.

Ubuntu에서는 sudo 그룹에 추가할 수 있다.

sudo usermod -aG sudo user1

이후 로그아웃/로그인 후 확인한다.

또는 필요한 경우:
/etc/sudoers

설정을 visudo로 수정한다.

sudo visudo

실무에서는 모든 sudo 권한을 주기보다
필요한 명령만 허용하는 방식도 사용할 수 있다.

## 면접문제
[리눅스 2장 면접 질문 3문제]

1. chmod와 chown의 차이를 설명해주세요.

정답:
chmod는 파일이나 디렉터리의 권한을 변경하는 명령이고,
chown은 파일이나 디렉터리의 소유자 또는 소유 그룹을 변경하는 명령입니다.


2. Linux에서 파일의 755 권한은 무엇을 의미합니까?

정답:
Owner는 rwx 권한을 가지며,
Group과 Other는 r-x 권한을 가집니다.

즉:
Owner = 읽기/쓰기/실행
Group = 읽기/실행
Other = 읽기/실행


3. Tomcat이나 Nginx 같은 서비스를 root가 아니라
전용 서비스 계정으로 실행하는 이유는 무엇입니까?

정답:
서비스가 취약점 등으로 침해되었을 때
공격자가 root 권한까지 얻는 위험을 줄이기 위해서입니다.

서비스에 필요한 최소 권한만 가진 전용 계정을 사용하면
문제가 발생했을 때 피해 범위를 제한할 수 있습니다.

또 사람이 직접 로그인할 필요가 없다면
nologin을 설정해 로그인 경로도 차단할 수 있습니다.
</details>

<details>
<summary><h2>3장 프로세스 서비스 systemd  로그관리</h2></summary>

## 프로그램과 프로세스
1. 프로그램은 디스크에 저장되어 있는 실행 파일이다.
2. 프로그램 = 실행되기 전 파일
3. 프로세스 = 현재 실행 중인 프로그램

## PID와 PPID
1. 실행 중인 프로세스를 구분하기 위해 숫자를 붙인게 PID
2. ps
3. ps aux
4. PPID : 부모 프로세스의 PID

## PID 1과 systemd
1. systemd는 Linux의 서비스와 부팅 과정을 관리하는 핵심 관리자
2. PID = 1

## Foreground와 Background
1. 명령을 실행했을 때 터미널을 계속 잡고 있는 것을 Foreground라고 합니다.
2. Background는 프로세스가 뒤에서 실행된다.
3. 명령 뒤에 &를 붙인다 : sleep 1000 &
4. Background 작업 확인 : jobs
5. Foreground로 가져오기 : fg
6. Background로 계속 실행 :bg

## ps로 프로세스 확인
1. ps
2. ps aux
3. ps -ef
4. pgrep nginx : PID 찾기
5. pgrep -a nginx : 프로세스 정보까지

## 프로세스 종료와 Signal
1. 실행 중인 프로세스를 종료할 때 : kill PID
2. kill -9 PID

## 서비스와 데몬
1. 데몬은 보통 백그라운드에서 계속 실행되면서 요청을 기다리는 프로그램이다.
2. 데몬을 운영체제 차원에서 관리하는 단위를 일반적으로 서비스라고 생각하면 된다.

## systemd와 systemctl
1. systemd가 서비스를 관리하고, systemd에게 명령할 때 사용하는 명령어가 systemctl이다.

## start와 enable 차이
1. start : 시작
2. enable : 다음 부팅 때 자동으로 시작되도록 설정

## 현재 실행과 자동 시작은 별개
1. systemctl status : 현재 상태
2. systemctl is-enabled : 부팅 자동 시작 여부

## Unit이란?
1. systemd는 여러 종류의 대상을 Unit이라는 단위로 관리한다.
2. .service : 서비스
3. .socket : 소켓
4. .mount : 마운트
5. .timer : 예약 작업
6. 지금 중요한건 service Unit이다.

## systemd 서비스 설정 파일
1. /etc/systemd/system
2. /usr/lib/systemd/system
3. /lib/systemd/system
4. systemd는 .service 파일을 보고 프로그램을 어떻게 시작할지 판단한다

## journalctl
1. systemd 서비스의 로그를 확인할 때 매우 중요한 명령이 journalctl이다.
2. 특정 서비스 로그 : journalctl -u nginx : journalctl -u nginx -n 50
3. 실시간 로그 : journalctl -f nginx
4. 최근 부팅 이후 로그만 : journalctl -b

## /var/log
1. 모든 로그가 journal에만 있는 것은 아니다.
2. 대표적인 위치

## 로그에서 자주 같이 사용하는 명령
1. tail -f 로그
2. grep -i "error" app.log
3. grep -E "ERROR|WARN|CRITICAL" app.log
4. tail -n 100 app.log

## 서비스 장애 확인 기본 순서
1. 서비스 상태 확인 : systemctl status
2. 프로세스 확인 : ps / pgrep
3. 포트 확인 : ss
4. 로그 확인 : journalctl /var/log
5. 설정/권한/자원 등 원인 확인
6. 조치
7. 서비스 정상 여부 재확인

## 확인문제
# Linux 3장 - 프로세스·서비스·systemd·로그 관리

## 확인문제 및 정답

### 1. 프로그램과 프로세스의 차이는 무엇인가?

**정답**

- 프로그램: 디스크에 저장되어 있는 실행 파일
- 프로세스: 프로그램이 실행되어 메모리에서 동작 중인 상태

---

### 2. PID란 무엇인가?

**정답**

PID는 Process ID의 약자로, 실행 중인 프로세스를 구분하기 위한 고유 번호이다.

예:

`PID 1500 → nginx`

---

### 3. PPID란 무엇인가?

**정답**

PPID는 Parent Process ID의 약자로, 현재 프로세스를 생성한 부모 프로세스의 PID이다.

---

### 4. Ubuntu에서 일반적으로 PID 1을 가지는 프로세스는 무엇인가?

**정답**

`systemd`

systemd는 시스템 부팅 및 서비스들을 관리한다.

---

### 5. Foreground와 Background 프로세스의 차이는 무엇인가?

**정답**

- Foreground: 현재 터미널을 점유하면서 실행되는 프로세스
- Background: 터미널 뒤에서 실행되는 프로세스

명령 뒤에 `&`를 붙이면 Background로 실행할 수 있다.

예:

`sleep 1000 &`

---

### 6. 실행 중인 프로세스를 확인하는 대표적인 명령어는 무엇인가?

**정답**

`ps aux`

또는

`ps -ef`

특정 프로세스를 검색할 때:

`ps aux | grep nginx`

또는

`pgrep -a nginx`

---

### 7. kill 명령어는 어떤 역할을 하는가?

**정답**

프로세스에게 Signal을 전달하는 명령어이다.

일반적으로:

`kill PID`

를 실행하면 SIGTERM을 전달하여 정상 종료를 요청한다.

---

### 8. SIGTERM과 SIGKILL의 차이는 무엇인가?

**정답**

- SIGTERM(15): 프로세스에게 정상적으로 종료할 것을 요청
- SIGKILL(9): 프로세스를 즉시 강제 종료

예:

`kill PID`

`kill -9 PID`

가능하면 SIGTERM으로 먼저 종료를 시도하고, 종료되지 않을 경우 SIGKILL을 사용한다.

---

### 9. 데몬(Daemon)이란 무엇인가?

**정답**

백그라운드에서 계속 실행되면서 요청을 기다리는 프로그램이다.

예:

- sshd
- nginx
- mysqld

---

### 10. systemd란 무엇인가?

**정답**

Linux 시스템의 부팅과 서비스 등을 관리하는 시스템 및 서비스 관리자이다.

Ubuntu에서 일반적으로 PID 1로 실행된다.

---

### 11. systemctl은 어떤 명령어인가?

**정답**

systemd가 관리하는 서비스를 제어하고 상태를 확인하는 명령어이다.

대표 명령:

- `systemctl start nginx`
- `systemctl stop nginx`
- `systemctl restart nginx`
- `systemctl status nginx`

---

### 12. systemctl start와 enable의 차이는 무엇인가?

**정답**

`start`

현재 서비스를 즉시 실행한다.

`enable`

서버가 부팅될 때 서비스를 자동으로 시작하도록 설정한다.

즉:

- start = 지금 실행
- enable = 부팅 시 자동 실행

---

### 13. stop과 disable의 차이는 무엇인가?

**정답**

`stop`

현재 실행 중인 서비스를 중지한다.

`disable`

다음 부팅부터 자동으로 실행되지 않도록 설정한다.

---

### 14. 서비스가 부팅 시 자동 시작하도록 설정되어 있는지 확인하는 명령어는?

**정답**

`systemctl is-enabled 서비스명`

예:

`systemctl is-enabled nginx`

---

### 15. systemd의 Unit이란 무엇인가?

**정답**

systemd가 관리하는 대상을 의미한다.

대표적인 Unit:

- `.service` → 서비스
- `.socket` → 소켓
- `.mount` → 마운트
- `.timer` → 예약 작업
- `.target` → 여러 Unit을 묶은 시스템 상태

---

### 16. 서비스 상태를 확인하는 명령어는?

**정답**

`systemctl status 서비스명`

예:

`systemctl status nginx`

주요 상태:

- active (running)
- inactive
- failed

---

### 17. journalctl은 어떤 명령어인가?

**정답**

systemd의 journal 로그를 확인하는 명령어이다.

특정 서비스 로그 확인:

`journalctl -u nginx`

최근 50줄:

`journalctl -u nginx -n 50`

실시간 확인:

`journalctl -u nginx -f`

---

### 18. Linux에서 일반적으로 로그 파일이 저장되는 디렉터리는 어디인가?

**정답**

`/var/log`

예:

- `/var/log/nginx/`
- `/var/log/apache2/`
- `/var/log/syslog`

---

### 19. 서비스 장애가 발생했을 때 기본적인 확인 순서는?

**정답**

1. 서비스 상태 확인
2. 프로세스 확인
3. 포트 확인
4. 로그 확인
5. 설정/권한/자원 등의 원인 확인
6. 조치
7. 정상 여부 재확인

대표 명령:

`systemctl status`

`ps` / `pgrep`

`ss`

`journalctl`

---

### 20. 서비스 장애가 발생했을 때 무조건 restart부터 하는 것이 좋지 않은 이유는?

**정답**

서비스를 바로 재시작하면 장애 당시의 상태나 로그 등 원인 분석에 필요한 정보가 사라질 수 있기 때문이다.

따라서 가능하면 먼저:

1. 상태 확인
2. 로그 확인
3. 오류 내용 확인
4. 원인 분석

을 한 뒤 필요한 경우 서비스를 재시작한다.


# Linux 3장 - 프로세스·서비스·systemd·로그 관리

## 1. 기본 실습

### 문제 1
현재 실행 중인 프로세스를 전체적으로 확인하시오.

정답:
```bash
ps aux
```

또는

```bash
ps -ef
```

---

### 문제 2
현재 실행 중인 SSH 관련 프로세스를 확인하시오.

정답:
```bash
ps aux | grep ssh
```

또는

```bash
pgrep -a sshd
```

---

### 문제 3
sshd 프로세스의 PID를 확인하시오.

정답:
```bash
pgrep sshd
```

프로세스 이름까지 같이 확인하려면:

```bash
pgrep -a sshd
```

---

### 문제 4
Ubuntu에서 SSH 서비스의 현재 상태를 확인하시오.

정답:
```bash
systemctl status ssh
```

주요 상태:
- active (running): 정상 실행 중
- inactive: 중지 상태
- failed: 실행 실패

---

### 문제 5
SSH 서비스가 부팅 시 자동으로 시작되도록 설정되어 있는지 확인하시오.

정답:
```bash
systemctl is-enabled ssh
```

결과 예:
```text
enabled
```

또는

```text
disabled
```

---

### 문제 6
SSH 서비스의 최근 로그 30줄을 확인하시오.

정답:
```bash
journalctl -u ssh -n 30
```

---

### 문제 7
SSH 서비스의 로그를 실시간으로 확인하시오.

정답:
```bash
journalctl -u ssh -f
```

종료:
```text
Ctrl + C
```

---

### 문제 8
`sleep 300` 명령을 Background로 실행하고 PID를 확인한 뒤 정상 종료하시오.

정답:

Background 실행:
```bash
sleep 300 &
```

PID 확인:
```bash
echo $!
```

또는

```bash
pgrep -a sleep
```

정상 종료:
```bash
kill PID
```

예:
```bash
kill 1234
```

---

# 2. 실무형 실습

### 문제 1
SSH 서비스의 현재 상태와 부팅 시 자동 시작 여부를 각각 확인하시오.

정답:

현재 상태:
```bash
systemctl status ssh
```

또는
```bash
systemctl is-active ssh
```

자동 시작 여부:
```bash
systemctl is-enabled ssh
```

핵심:
```text
active
= 현재 실행 상태

enabled
= 부팅 시 자동 시작 설정
```

---

### 문제 2
테스트용 서비스가 현재 실행 중이지만 부팅 시 자동 실행되지 않는 상황이다.

현재 실행 여부와 자동 시작 여부를 각각 확인하고 자동 시작을 설정하시오.

정답:

현재 실행 여부:
```bash
systemctl status 서비스명
```

자동 시작 여부:
```bash
systemctl is-enabled 서비스명
```

자동 시작 설정:
```bash
sudo systemctl enable 서비스명
```

필요하면 현재 서비스도 시작:
```bash
sudo systemctl start 서비스명
```

한 번에 현재 시작 + 자동 시작:
```bash
sudo systemctl enable --now 서비스명
```

---

### 문제 3
서비스 설정을 변경한 뒤 서비스를 다시 적용하려고 한다.

서비스가 reload를 지원하는 경우 프로세스를 완전히 중지하지 않고 설정을 다시 읽도록 하시오.

정답:
```bash
sudo systemctl reload 서비스명
```

예:
```bash
sudo systemctl reload nginx
```

서비스가 reload를 지원하지 않거나 완전 재시작이 필요한 경우:
```bash
sudo systemctl restart 서비스명
```

차이:
```text
reload
= 프로세스를 유지하면서 설정 다시 읽기

restart
= 프로세스를 종료하고 다시 시작
```

---

### 문제 4
특정 서비스의 최근 100줄 로그에서 ERROR라는 문자열만 확인하시오.

정답:
```bash
journalctl -u 서비스명 -n 100 | grep -i "error"
```

예:
```bash
journalctl -u nginx -n 100 | grep -i "error"
```

---

### 문제 5
서버가 재부팅된 이후 발생한 systemd 로그만 확인하시오.

정답:
```bash
journalctl -b
```

특정 서비스의 현재 부팅 이후 로그:
```bash
journalctl -b -u 서비스명
```

예:
```bash
journalctl -b -u ssh
```

---

# 3. 장애 대응 문제

### 문제 1
웹 서비스에 접속되지 않는다.

`systemctl status nginx` 결과가 다음과 같다.

```text
Active: failed
```

어떤 순서로 확인하겠는가?

정답:

서비스 상태 확인:
```bash
systemctl status nginx
```

로그 확인:
```bash
journalctl -u nginx -n 50
```

애플리케이션 자체 로그 확인:
```bash
tail -n 50 /var/log/nginx/error.log
```

필요하면 설정 파일 문법, 권한, 포트 충돌 등을 확인한다.

기본 흐름:
```text
상태 확인
→ 로그 확인
→ 원인 분석
→ 수정
→ 서비스 시작
→ 정상 여부 재확인
```

---

### 문제 2
서비스 상태는 `active (running)`인데 사용자가 웹페이지에 접속하지 못한다고 한다.

서비스가 실행 중이라는 이유만으로 정상이라고 판단해도 되는가?

정답:

안 된다.

실제 포트가 LISTEN 상태인지 확인해야 한다.

```bash
ss -lntp
```

필요하면:
```bash
curl localhost
```

점검 흐름:
```text
서비스 상태
→ 프로세스
→ 포트
→ 애플리케이션 응답
→ 네트워크/방화벽
```

---

### 문제 3
프로세스가 비정상적으로 멈춰서 종료하려고 한다.

처음부터 `kill -9`를 사용해도 되는가?

정답:

가능하면 처음부터 사용하지 않는다.

먼저:
```bash
kill PID
```

로 SIGTERM을 보내 정상 종료를 요청한다.

종료되지 않을 경우:
```bash
kill -9 PID
```

를 사용한다.

이유:
SIGKILL은 프로세스가 정상 종료 작업을 수행할 기회를 주지 않고 즉시 종료하기 때문이다.

---

### 문제 4
Nginx 서비스를 `start`하여 정상적으로 사용하고 있었다.

서버 재부팅 후 Nginx가 실행되지 않았다.

가장 먼저 의심할 부분은?

정답:

부팅 자동 시작 설정 여부를 확인한다.

```bash
systemctl is-enabled nginx
```

disabled라면:
```bash
sudo systemctl enable nginx
```

현재 실행도 필요하다면:
```bash
sudo systemctl start nginx
```

또는:
```bash
sudo systemctl enable --now nginx
```

핵심:
```text
start ≠ enable

start
= 현재 실행

enable
= 부팅 시 자동 시작
```

---

### 문제 5
서비스 장애가 발생하자 담당자가 바로 다음 명령을 실행했다.

```bash
sudo systemctl restart app
```

왜 이 방식이 항상 좋은 대응은 아닌가?

정답:

서비스를 바로 재시작하면 장애 당시 상태나 원인 분석에 필요한 정보가 사라질 수 있기 때문이다.

먼저:
```bash
systemctl status app
```

로그 확인:
```bash
journalctl -u app -n 100
```

프로세스/포트 확인:
```bash
ps aux | grep app
ss -lntp
```

권장 흐름:
```text
현상 확인
→ 상태 확인
→ 로그 확인
→ 증거 확보
→ 원인 분석
→ 조치
→ 재확인
```

---

# 4. 면접 질문

### 문제 1
프로그램과 프로세스의 차이를 설명해주세요.

정답:

프로그램은 디스크에 저장된 실행 가능한 파일이고,
프로세스는 그 프로그램이 실행되어 메모리에서 동작하고 있는 상태입니다.

---

### 문제 2
systemd, systemctl, service의 관계를 설명해주세요.

정답:

systemd는 Linux의 시스템과 서비스를 관리하는 관리자입니다.

`.service` 파일은 systemd에게 해당 프로그램을 어떻게 실행하고 관리할지 알려주는 설정입니다.

systemctl은 사용자가 systemd에게 서비스 시작, 중지, 상태 확인 등의 명령을 전달하는 도구입니다.

흐름:
```text
사용자
→ systemctl
→ systemd
→ xxx.service
→ 프로그램 실행
→ 프로세스
```

---

### 문제 3
`systemctl start`와 `systemctl enable`의 차이는 무엇입니까?

정답:

`start`
= 서비스를 현재 즉시 실행

`enable`
= 서버가 부팅될 때 해당 서비스가 자동으로 시작되도록 설정

---

### 문제 4
SIGTERM과 SIGKILL의 차이를 설명해주세요.

정답:

SIGTERM은 프로세스에게 정상적으로 종료할 것을 요청하는 Signal입니다.

SIGKILL은 프로세스를 즉시 강제로 종료하는 Signal입니다.

일반적으로 먼저 SIGTERM으로 종료를 시도하고,
종료되지 않을 경우 SIGKILL을 마지막 수단으로 사용합니다.

---

### 문제 5
Linux 서버에서 서비스 장애가 발생했을 때 어떤 순서로 확인하시겠습니까?

정답:

먼저 서비스 상태를 확인합니다.

```bash
systemctl status 서비스명
```

그다음 프로세스와 포트를 확인합니다.

```bash
ps
pgrep
ss
```

그리고 systemd 로그와 애플리케이션 로그를 확인합니다.

```bash
journalctl -u 서비스명
```

```text
/var/log
```

기본 흐름:
```text
상태 확인
→ 프로세스 확인
→ 포트 확인
→ 로그 확인
→ 원인 분석
→ 조치
→ 재확인
```

---

# 5. 3장 핵심 명령어

```bash
# 프로세스 확인
ps aux
ps -ef
pgrep -a 프로세스명

# 프로세스 종료
kill PID
kill -9 PID

# 서비스 상태
systemctl status 서비스명
systemctl is-active 서비스명

# 서비스 제어
sudo systemctl start 서비스명
sudo systemctl stop 서비스명
sudo systemctl restart 서비스명
sudo systemctl reload 서비스명

# 부팅 자동 시작
sudo systemctl enable 서비스명
sudo systemctl disable 서비스명
systemctl is-enabled 서비스명

# 현재 시작 + 자동 시작
sudo systemctl enable --now 서비스명

# systemd 로그
journalctl -u 서비스명
journalctl -u 서비스명 -n 50
journalctl -u 서비스명 -f
journalctl -b
```

# 6. 3장 완료 기준

- 프로그램과 프로세스 차이를 설명할 수 있다.
- PID / PPID를 이해한다.
- 프로세스를 확인하고 종료할 수 있다.
- systemd / systemctl / service의 관계를 설명할 수 있다.
- start와 enable의 차이를 설명할 수 있다.
- systemctl로 서비스를 관리할 수 있다.
- journalctl로 서비스 로그를 확인할 수 있다.
- 서비스 장애 시 상태 → 프로세스 → 포트 → 로그 순서로 접근할 수 있다.

</details>

<details>
<summary><h2>4장 가상화와 가상머신</h2></summary>
   # Linux 4장 - 가상화와 가상머신

---

# 1. 개념 요약

## 1.1 가상화란?

가상화는 하나의 물리 서버 자원을 여러 개의 논리적인 서버처럼 나누어 사용하는 기술이다.

예:

```text
Physical Server

CPU 16 Core
RAM 64GB
Disk 2TB

      ↓ 가상화

VM1 - Ubuntu
VM2 - Windows
VM3 - Ubuntu
```

물리 자원을 효율적으로 사용할 수 있고,
여러 서버 환경을 하나의 물리 장비에서 운영할 수 있다.

---

## 1.2 Host와 Guest

```text
Host
= VM을 실행시키는 쪽

Guest
= VM 안에서 실행되는 운영체제
```

예:

```text
Windows PC
↓
VMware Workstation
↓
Ubuntu VM
```

- Windows = Host OS
- Ubuntu = Guest OS

---

## 1.3 Hypervisor

Hypervisor는 물리 자원을 VM에 나누어 제공하고
VM을 생성·실행·관리하는 계층이다.

```text
VM1        VM2        VM3
 |          |          |
 +----------+----------+
            |
       Hypervisor
            |
     Physical Hardware
```

주요 역할:

- CPU 할당
- Memory 할당
- Disk 제공
- Virtual NIC 제공
- VM 격리
- VM 실행/중지

---

## 1.4 Type 1 / Type 2 Hypervisor

### Type 1

물리 하드웨어 위에서 직접 동작하는 서버 가상화 방식이다.

대표적인 예:

- VMware ESXi
- Hyper-V Server 계열
- KVM 기반 서버 가상화 환경

주로 데이터센터나 서버 가상화 환경에서 사용한다.

### Type 2

기존 운영체제 위에 가상화 프로그램을 설치하는 방식이다.

예:

```text
VM
↓
VMware Workstation
↓
Windows
↓
Hardware
```

대표적인 예:

- VMware Workstation
- VirtualBox

개발, 테스트, 개인 실습 환경에서 많이 사용한다.

---

## 1.5 VM의 가상 하드웨어

VM 안에서는 실제 서버처럼 다음 자원을 볼 수 있다.

```text
vCPU
Virtual Memory
Virtual Disk
Virtual NIC
```

Guest OS에서는 실제 하드웨어처럼 사용할 수 있다.

확인 예:

```bash
lscpu
free -h
lsblk
ip addr
```

---

## 1.6 vCPU와 Overcommit

vCPU는 VM에 할당된 논리적인 CPU 자원이다.

예:

```text
Physical CPU = 8 Core

VM1 = 4 vCPU
VM2 = 4 vCPU
VM3 = 4 vCPU
```

총 12 vCPU를 할당할 수도 있다.

이를 자원 Overcommit 관점에서 볼 수 있다.

VM들이 동시에 CPU를 많이 사용하면
물리 CPU를 서로 경쟁하기 때문에 성능 저하가 발생할 수 있다.

---

## 1.7 가상 메모리

Host의 물리 RAM을 VM에 나누어 할당한다.

예:

```text
Host RAM = 32GB

VM1 = 8GB
VM2 = 8GB
VM3 = 8GB
```

Host OS도 메모리가 필요하므로
VM에 모든 RAM을 할당하면 안 된다.

---

## 1.8 Virtual Disk

VM에서 `/dev/sda`, `/dev/sdb`처럼 보이는 디스크는
실제로는 Host의 저장공간 위에 생성된 가상 디스크일 수 있다.

```text
Host SSD
↓
Virtual Disk File
↓
VM
↓
/dev/sda
```

Guest OS에서는 일반 디스크처럼:

- Partition
- Filesystem
- Mount
- LVM

등을 사용할 수 있다.

---

## 1.9 Thin / Thick Provisioning

### Thick

지정한 디스크 공간을 미리 확보하는 방식이다.

예:

```text
VM Disk = 100GB
실제 Host 공간도 100GB 확보
```

### Thin

VM에서는 100GB로 보이더라도
실제로 사용한 만큼 Host 저장공간을 소비한다.

예:

```text
VM Disk = 100GB
실제 사용 = 20GB
Host 사용량 ≈ 실제 사용량 중심
```

장점:

- 저장공간 효율

주의:

- 실제 Host Disk보다 VM에 너무 많은 논리 용량을 할당하면
  나중에 Host 저장공간 부족 장애가 발생할 수 있다.

---

## 1.10 Virtual NIC / Virtual Switch

VM도 네트워크 인터페이스를 가진다.

예:

```text
ens32
ens34
ens35
```

실제 랜카드가 아니라 Virtual NIC이다.

```text
VM
↓
Virtual NIC
↓
Virtual Switch
↓
Host / Physical Network
```

Virtual Switch는 VM끼리 또는 VM과 외부 네트워크를 연결한다.

---

## 1.11 NAT / Bridged / Host-only

### NAT

VM이 Host를 통해 외부 네트워크로 통신한다.

```text
VM
↓
Host NAT
↓
Internet
```

### Bridged

VM이 물리 네트워크에 직접 연결된 별도의 장비처럼 동작한다.

```text
VM
↓
Physical Network
```

### Host-only

Host와 VM 또는 같은 가상 네트워크의 VM끼리 주로 통신한다.

외부 네트워크와 분리된 실습 환경을 만들 때 유용하다.

---

## 1.12 Snapshot

Snapshot은 VM의 특정 시점 상태를 저장해
나중에 해당 상태로 되돌릴 수 있게 하는 기능이다.

예:

```text
정상 상태
↓
Snapshot
↓
방화벽 실습
↓
네트워크 장애
↓
Snapshot 복원
```

중요:

```text
Snapshot ≠ Backup
```

Snapshot은 실습이나 변경 전 되돌리기 용도로 유용하지만
독립적인 백업을 완전히 대체하지는 않는다.

---

## 1.13 Clone

Clone은 기존 VM을 복제하여 새로운 VM을 만드는 기능이다.

예:

```text
Base Ubuntu VM
├── web01
├── web02
├── was01
└── was02
```

복제 후 확인해야 할 것:

- Hostname
- IP
- Machine ID
- SSH Host Key
- 서비스 설정

---

## 1.14 KVM

KVM은 Kernel-based Virtual Machine의 약자이다.

Linux Kernel에 가상화 기능을 제공하여
Linux 서버에서 VM을 실행할 수 있게 한다.

구조:

```text
VM
↓
QEMU / KVM
↓
Linux Kernel
↓
Hardware
```

KVM은 Linux의 하드웨어 가상화 기능을 담당하고
QEMU와 함께 사용하는 경우가 많다.

---

## 1.15 virt-manager

virt-manager는 KVM/QEMU 기반 VM을 GUI로 관리하는 도구이다.

주요 기능:

- VM 생성
- CPU 설정
- Memory 설정
- Disk 설정
- Network 설정
- VM 시작/종료

```text
virt-manager
= 관리 GUI

KVM/QEMU
= 실제 가상화 기능
```

---

## 1.16 Hardware Virtualization

CPU 자체에서도 가상화를 지원한다.

대표적인 기능:

```text
Intel VT-x
AMD-V
```

BIOS/UEFI에서 비활성화되어 있으면
가상화 기능이 정상적으로 동작하지 않을 수 있다.

확인 예:

```bash
lscpu
```

---

## 1.17 VM과 Container 차이

### VM

```text
Hardware
↓
Hypervisor
↓
Guest OS
↓
Application
```

VM마다 Guest OS가 존재한다.

### Container

```text
Hardware
↓
Host OS Kernel
↓
Container Runtime
↓
Container
```

Container는 Host Kernel을 공유한다.

일반적인 특징:

```text
VM
- Guest OS 포함
- 비교적 무거움
- OS 단위 격리

Container
- Host Kernel 공유
- 가벼움
- 시작 속도가 빠름
```

---

## 1.18 가상화 장점

- 물리 서버 자원 활용률 향상
- 서버 구축 속도 향상
- 테스트 환경 생성 편리
- Snapshot/Clone 활용 가능
- 여러 OS 운영 가능
- 서버 통합 가능

---

## 1.19 가상화의 장애 위험

가상화 환경이라고 장애가 없어지는 것은 아니다.

```text
Physical Host 장애
       ↓
VM1    VM2    VM3
 ↓      ↓      ↓
장애    장애    장애
```

한 Hypervisor Host에 여러 VM이 있으면
Host 장애가 여러 VM에 동시에 영향을 줄 수 있다.

따라서 실제 환경에서는:

- 여러 Hypervisor Host
- HA
- Live Migration
- 이중화
- Backup

등을 고려한다.

---

# 2. 확인문제 + 정답

## 문제 1

가상화란 무엇인가?

### 정답

하나의 물리적인 컴퓨팅 자원을 여러 개의 논리적인 컴퓨팅 환경으로 나누어 사용하는 기술이다.

---

## 문제 2

Host와 Guest의 차이는 무엇인가?

### 정답

- Host: VM을 실행하고 관리하는 쪽
- Guest: VM 안에서 실행되는 운영체제

---

## 문제 3

Hypervisor의 역할은 무엇인가?

### 정답

물리 CPU, Memory, Disk, Network 등의 자원을 VM에 할당하고
VM을 생성·실행·관리하는 역할을 한다.

---

## 문제 4

Type 1과 Type 2 Hypervisor의 차이는?

### 정답

Type 1은 물리 하드웨어 위에서 직접 서버 가상화를 제공하는 방식이고,
Type 2는 기존 운영체제 위에 가상화 프로그램을 설치하는 방식이다.

---

## 문제 5

vCPU란 무엇인가?

### 정답

VM에 할당된 논리적인 CPU 자원이다.

---

## 문제 6

CPU Overcommit이란 무엇인가?

### 정답

물리 CPU 자원보다 많은 vCPU를 VM들에게 논리적으로 할당하는 것이다.

모든 VM이 동시에 높은 CPU를 사용하면 성능 저하가 발생할 수 있다.

---

## 문제 7

Thin Provisioning이란 무엇인가?

### 정답

VM에 큰 디스크 용량을 논리적으로 제공하되
실제 Host 저장공간은 VM이 사용하는 만큼 중심으로 소비하는 방식이다.

---

## 문제 8

NAT, Bridged, Host-only의 차이는 무엇인가?

### 정답

- NAT: Host를 통해 외부 네트워크로 통신
- Bridged: VM이 물리 네트워크의 독립 장비처럼 동작
- Host-only: Host와 VM 또는 가상 네트워크 내부 통신 중심

---

## 문제 9

Snapshot과 Backup의 차이는?

### 정답

Snapshot은 특정 시점으로 빠르게 되돌리기 위한 기능이고,
Backup은 원본 손실이나 장애에 대비하여 데이터를 별도로 보호하는 목적이다.

Snapshot은 Backup을 완전히 대체하지 않는다.

---

## 문제 10

Clone이란 무엇인가?

### 정답

기존 VM을 복제하여 새로운 VM을 만드는 기능이다.

---

## 문제 11

VM을 Clone한 후 확인해야 할 항목은?

### 정답

예:

- Hostname
- IP
- Machine ID
- SSH Host Key
- 서비스 설정

---

## 문제 12

KVM이란 무엇인가?

### 정답

Linux Kernel에 가상화 기능을 제공하여
Linux 환경에서 VM을 실행할 수 있게 하는 기술이다.

---

## 문제 13

virt-manager는 어떤 역할을 하는가?

### 정답

KVM/QEMU 기반의 가상머신을 GUI로 생성하고 관리하는 도구이다.

---

## 문제 14

Intel VT-x와 AMD-V는 무엇인가?

### 정답

CPU가 제공하는 하드웨어 가상화 지원 기능이다.

---

## 문제 15

VM과 Container의 가장 큰 구조적 차이는 무엇인가?

### 정답

VM은 VM마다 Guest OS를 가지지만,
Container는 기본적으로 Host OS의 Kernel을 공유한다.

---

# 3. 기본 실습문제 + 정답

## 문제 1

현재 VM의 CPU 정보를 확인하시오.

### 정답

```bash
lscpu
```

---

## 문제 2

현재 VM에 할당된 Memory 정보를 확인하시오.

### 정답

```bash
free -h
```

---

## 문제 3

VM의 가상 디스크 정보를 확인하시오.

### 정답

```bash
lsblk
```

또는

```bash
sudo fdisk -l
```

---

## 문제 4

VM의 Network Interface와 IP 주소를 확인하시오.

### 정답

```bash
ip addr
```

간단히 확인:

```bash
ip -br addr
```

---

## 문제 5

VM의 Hostname을 확인하시오.

### 정답

```bash
hostname
```

또는:

```bash
hostnamectl
```

---

## 문제 6

현재 Linux에서 가상화 관련 CPU 정보를 확인하시오.

### 정답

```bash
lscpu
```

출력에서 Virtualization 항목 등을 확인한다.

---

## 문제 7

현재 VM이 어떤 환경에서 실행되고 있는지 확인하는 명령어 중 하나를 사용하시오.

### 정답

```bash
systemd-detect-virt
```

환경에 따라 예:

```text
vmware
kvm
oracle
none
```

등이 출력될 수 있다.

---

## 문제 8

VM에 여러 NIC가 있다면 모든 Interface를 확인하시오.

### 정답

```bash
ip link
```

또는:

```bash
ip -br addr
```

---

# 4. 실무형 문제 + 정답

## 문제 1

VM이 느리다는 요청이 들어왔다.

VM 자체에 CPU와 Memory가 얼마나 할당되어 있는지 확인하려면?

### 정답

CPU:

```bash
lscpu
```

Memory:

```bash
free -h
```

필요하면 실제 사용률은:

```bash
top
```

으로 확인한다.

---

## 문제 2

VM에 100GB 디스크를 설정했는데
Host에서 실제로 20GB 정도만 사용하고 있다.

어떤 가상 디스크 방식일 가능성이 높은가?

### 정답

Thin Provisioning일 가능성이 높다.

VM에서는 100GB로 보이지만
Host에서는 실제 사용량을 중심으로 공간을 소비할 수 있다.

---

## 문제 3

새 VM을 기존 VM에서 Clone했다.

부팅 후 가장 먼저 확인할 시스템 정보는?

### 정답

대표적으로:

```bash
hostnamectl
ip addr
```

확인해야 할 항목:

- Hostname
- IP 주소
- Network 설정
- Machine ID
- SSH Host Key

중복 여부를 점검한다.

---

## 문제 4

테스트 전에 iptables 설정을 크게 변경하려고 한다.

빠르게 이전 상태로 되돌릴 가능성이 필요하다.

가상화 환경에서 어떤 기능을 사용할 수 있는가?

### 정답

Snapshot을 사용할 수 있다.

변경 전 Snapshot을 생성하고
실습 실패 시 이전 상태로 복원할 수 있다.

단, Snapshot을 장기 백업으로 사용해서는 안 된다.

---

## 문제 5

Host 물리 RAM이 16GB인데
VM 3개에 각각 8GB씩 RAM을 할당하였다.

어떤 문제가 발생할 수 있는가?

### 정답

VM RAM 총합이 24GB로
Host 물리 RAM 16GB보다 크다.

VM들이 동시에 메모리를 많이 사용하면
Host의 Memory 부족, Swap 증가, 성능 저하 등이 발생할 수 있다.

---

## 문제 6

외부 인터넷과 분리된 Linux 네트워크 실습 환경을 만들고 싶다.

어떤 VMware 네트워크 방식이 적합한가?

### 정답

Host-only 방식이 적합할 수 있다.

Host와 VM 또는 동일한 Host-only 네트워크의 VM끼리
통신하도록 구성할 수 있다.

---

# 5. 장애 대응 문제 + 정답

## 문제 1

VM이 부팅되지 않는다.

가장 먼저 어떤 부분들을 확인할 수 있는가?

### 정답

확인 순서 예:

```text
VM 전원 상태
↓
Hypervisor 오류 메시지
↓
Host CPU / Memory / Disk 여유 공간
↓
Virtual Disk 연결 여부
↓
VM 설정
↓
Guest OS 부팅 로그
```

Host의 자원 부족이나 Virtual Disk 문제도 함께 확인한다.

---

## 문제 2

VM 여러 대가 동시에 매우 느려졌다.

각 VM 내부에서는 특별한 문제가 보이지 않는다.

어떤 부분을 의심할 수 있는가?

### 정답

Hypervisor Host의 자원 부족을 의심할 수 있다.

예:

- Physical CPU 부족
- CPU Overcommit
- Memory 부족
- Host Swap 증가
- Storage I/O 병목
- Host Disk 용량 부족

여러 VM이 동시에 느려졌다면
각 Guest뿐 아니라 Host 계층도 확인해야 한다.

---

## 문제 3

한 물리 Hypervisor Host 위에 VM 10대가 있다.

Host가 갑자기 장애로 종료되었다.

VM에는 어떤 영향이 발생하는가?

### 정답

해당 Host에서 실행 중이던 VM들이 모두 영향을 받을 수 있다.

가상화는 VM을 논리적으로 분리하지만
물리 Host 자체의 장애까지 제거하는 것은 아니다.

따라서 운영 환경에서는 HA 및 Host 이중화를 고려한다.

---

## 문제 4

VM을 Clone한 뒤 두 VM이 네트워크에서 충돌한다.

가장 먼저 무엇을 확인해야 하는가?

### 정답

두 VM의 IP 설정을 확인한다.

```bash
ip addr
ip route
```

또한:

- Hostname
- MAC 설정
- Machine ID
- Network 설정

등의 중복 여부도 확인한다.

---

## 문제 5

Thin Provisioning으로 여러 VM에 많은 디스크를 할당해 두었다.

어느 날 여러 VM에서 동시에 디스크 관련 장애가 발생했다.

Host에서 무엇을 확인해야 하는가?

### 정답

Host의 실제 물리 Disk 여유 공간을 확인해야 한다.

Thin Provisioning은 논리적으로 실제 용량보다 많은 공간을 할당할 수 있기 때문에
VM들이 동시에 디스크를 많이 사용하면 Host Storage가 고갈될 수 있다.

---

## 문제 6

VM의 NIC는 정상적으로 보이지만 외부 통신이 되지 않는다.

가상화 계층에서 확인할 항목은?

### 정답

예:

- Virtual NIC가 연결되어 있는지
- VMnet 설정
- NAT / Bridged / Host-only 설정
- Virtual Switch 연결
- Host Network 상태

Guest 내부에서는:

```bash
ip addr
ip route
ping
```

등도 확인한다.

---

# 6. 면접질문 + 정답

## 질문 1

가상화를 사용하는 이유를 설명해주세요.

### 정답

하나의 물리 서버 자원을 여러 VM으로 나누어 사용함으로써
자원 활용률을 높이고 서버 구축 및 운영을 편리하게 할 수 있습니다.

또한 Snapshot, Clone 등을 활용하여
테스트 환경 구성과 서버 복제가 편리합니다.

---

## 질문 2

Type 1과 Type 2 Hypervisor의 차이는 무엇입니까?

### 정답

Type 1은 서버 가상화를 위해 하드웨어에 가까운 계층에서 동작하며
데이터센터와 서버 환경에 주로 사용됩니다.

Type 2는 Windows 같은 기존 운영체제 위에 가상화 프로그램을 설치하여
VM을 실행하는 방식이며 개발, 테스트, 개인 실습에 많이 사용됩니다.

---

## 질문 3

VM과 Container의 차이는 무엇입니까?

### 정답

VM은 각 VM마다 Guest OS를 포함하지만,
Container는 Host OS의 Kernel을 공유합니다.

따라서 Container가 일반적으로 더 가볍고 빠르게 시작되지만,
VM은 OS 단위의 격리와 서로 다른 운영체제 사용에 유리합니다.

---

## 질문 4

Snapshot과 Backup의 차이는 무엇입니까?

### 정답

Snapshot은 VM의 특정 시점 상태로 빠르게 되돌리기 위한 기능입니다.

Backup은 시스템이나 데이터가 손실되었을 때 복구하기 위해
원본과 별도로 데이터를 보호하는 것이 목적입니다.

Snapshot은 Backup을 완전히 대체할 수 없습니다.

---

## 질문 5

Thin Provisioning의 장점과 위험은 무엇입니까?

### 정답

장점은 실제 사용하는 만큼 중심으로 저장공간을 소비하여
스토리지를 효율적으로 사용할 수 있다는 것입니다.

하지만 실제 물리 스토리지보다 많은 논리 용량을 할당할 수 있기 때문에
VM들의 사용량이 증가하면 Host의 실제 저장공간이 부족해질 수 있습니다.

---

## 질문 6

VM을 Clone한 후 어떤 점을 확인해야 합니까?

### 정답

Hostname, IP 주소, Machine ID, SSH Host Key 등
시스템 식별 정보가 기존 VM과 중복되지 않는지 확인해야 합니다.

특히 IP 중복은 네트워크 장애를 발생시킬 수 있습니다.

---

## 질문 7

KVM과 virt-manager의 관계를 설명해주세요.

### 정답

KVM은 Linux Kernel에서 가상화 기능을 제공하는 기술이고,
virt-manager는 KVM/QEMU 환경의 VM을 GUI로 생성하고 관리하기 위한 도구입니다.

---

## 질문 8

가상화 환경에서 Host 장애가 중요한 이유는 무엇입니까?

### 정답

하나의 Host 위에 여러 VM이 실행될 수 있기 때문에
Host 자체가 장애가 나면 해당 Host의 여러 VM이 동시에 영향을 받을 수 있습니다.

그래서 실제 운영 환경에서는
Host 이중화, HA, Migration, Backup 등을 고려합니다.

---

# 7. 핵심 명령어 정리

```bash
# CPU
lscpu

# Memory
free -h

# Disk
lsblk
sudo fdisk -l

# Network
ip addr
ip -br addr
ip link
ip route

# Hostname
hostname
hostnamectl

# 가상화 환경 확인
systemd-detect-virt
```

---

# 8. 4장 완료 기준

아래 내용을 설명할 수 있으면 4장 기본 개념은 완료한 것으로 본다.

- 가상화가 무엇인지 설명할 수 있다.
- Host와 Guest의 차이를 설명할 수 있다.
- Hypervisor의 역할을 설명할 수 있다.
- Type 1 / Type 2 차이를 설명할 수 있다.
- vCPU / Virtual Memory / Virtual Disk / Virtual NIC를 이해한다.
- CPU / Memory Overcommit의 위험을 이해한다.
- Thin / Thick Provisioning 차이를 설명할 수 있다.
- NAT / Bridged / Host-only 차이를 설명할 수 있다.
- Snapshot과 Backup의 차이를 설명할 수 있다.
- Clone 후 중복 설정을 확인해야 하는 이유를 안다.
- KVM과 virt-manager의 관계를 설명할 수 있다.
- VM과 Container의 차이를 설명할 수 있다.
- VM 장애뿐 아니라 Hypervisor Host 장애도 생각할 수 있다.
   

</details>








