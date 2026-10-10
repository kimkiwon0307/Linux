# 리눅스

## 리눅스 디렉터리 구조

/etc : 시스템/서비스 설정 파일
/var : 계속 변하는 데이터 로그, 캐시 등
/home : 일반 사용자 홈 디렉터리
/tmp : 임시 파일
/opt : 별도로 설치하는 프로그램을 두기도 함
/dev : 디스크, 터미널 같은 장치를 파일 형태로 표현
/proc : 프로세스와 커널 정보를 보여주는 가상 파일 시스템

## 절대경로와 상대경로
/ : 절대 경로
상대 경로 : 현재 위치를 기준으로
.. : 상위 디렉터리
. : 현재 디렉터리
~ : 사용자의 홈 디렉터리

## 파일과 디렉터리 기본 명령
현재 위치가 어디지? : pwd
여기 뭐가 있지? : ls
숨김 파일까지? : ls -la
디렉터리 이동 : cd
디렉터리 생성 : mkdir
빈 파일 생성 : touch
복사 : cp
이동/이름 변경 : mv
삭제 : rm

## 파일 내용 확인
전체 내용 간단히 확인 : cat
긴 파일 페이지 단위 확인 : less
앞 부분 확인 : head
마지막 부분 확인 : tail
실시간 로그 확인: tail -f

## 파일 찾기와 내용 검색
파일 자체를 찾음 : find
파일 안의 문자열을 찾음 : grep

## 파이프 | 
앞 명령어의 결과를 뒤 명령어의 입력으로 전달

## > 와 >>
덮어 쓰기 : >
뒤에 추가 : >>

## 문제
1. Linux에서 시스템이나 서비스 설정 파일이 주로 저장되는 디렉터리는?
2. 시스템 로그가 주로 저장되는 디렉터리는?
3. 현재 작업 중인 경로를 확인하는 명령어는?
4. 숨김 파일까지 포함해서 파일 목록을 자세히 확인하려면?
5. /var/log 안에서 이름에 nginx가 들어간 파일을 찾으려면 어떤 명령어를 사용하나요?
6. app.log에서 ERROR라는 문자열이 들어간 줄만 확인하려면?
7. app.log의 마지막 부분을 실시간으로 계속 보고 싶다면?
8. `>`와 `>>`의 차이는?
9. `ps aux | grep nginx`에서 `|`는 무슨 역할인가요?
10. 현재 위치가 /home/ubuntu일 때 상위 디렉터리로 이동하려면?

## 실습 문제
1. 홈 디렉터리로 이동한다.
2. linux-day1이라는 디렉터리를 만든다.
3. linux-day1 안에
   app.log
   config.conf
   test.txt
   세 파일을 만든다.
4. app.log 안에 아래 내용을 넣는다.
INFO server started
INFO user login
ERROR database connection failed
WARN memory usage high
ERROR timeout occurred
5. app.log에서 ERROR가 포함된 줄만 출력한다.
6. linux-day1 안에서 이름에 conf가 포함된 파일을 find로 찾는다.
7. app.log의 마지막 2줄만 출력한다.
8. ERROR가 포함된 결과를 error.log 파일에 저장한다.
9. error.log에
   ERROR disk full
   이라는 내용을 기존 내용을 지우지 않고 추가한다.
10. 최종적으로 linux-day1 안의 파일 목록을 자세히 확인한다.

## 정답
cd ~

mkdir linux-day1

touch ./linux-day1/app.log ./linux-day1/config.conf ./linux-day1/test.txt

cat > ./linux-day1/app.log << 'EOF'
INFO server started
INFO user login
ERROR database connection failed
WARN memory usage high
ERROR timeout occurred
EOF

grep "ERROR" ./linux-day1/app.log

find ./linux-day1 -name "*conf*"

tail -n 2 ./linux-day1/app.log

grep "ERROR" ./linux-day1/app.log > ./linux-day1/error.log

echo "ERROR disk full" >> ./linux-day1/error.log

ls -al ./linux-day1/

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
















