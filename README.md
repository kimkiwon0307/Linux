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


</details>










