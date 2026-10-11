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














