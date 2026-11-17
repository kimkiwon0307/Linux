<img width="1122" height="1402" alt="image" src="https://github.com/user-attachments/assets/daa824c0-403a-4c3a-80e4-1a39af6445f7" />



# Linux 프로젝트 — 2장 1교시
## Linux 파일·디렉터리 구조 및 기본 명령어

### 학습 환경

| 항목 | 내용 |
|---|---|
| OS | Ubuntu Server 24.04 LTS |
| 가상화 | VMware Workstation |
| 서버 | linux01 |
| 사용자 | infra |
| 학습 방식 | 개념 → 원리 → 명령어 → 실습 → 검증 → 장애 대응 |

### 학습 목표

- Linux 파일시스템 구조 이해
- 절대경로와 상대경로 구분
- 파일·디렉터리 생성, 복사, 이동, 삭제
- 로그 및 설정 파일 내용 조회
- `find`와 `grep` 활용
- 파이프와 리다이렉션 이해
- 심볼릭 링크와 하드 링크 이해
- `tar`를 이용한 압축·복원
- 기본적인 파일 관련 장애 대응

---

# 1. Linux 파일시스템 구조

## 1.1 Linux 파일시스템이란?

Linux는 루트 디렉터리 `/`를 기준으로
모든 파일과 디렉터리가 계층적으로 연결된다.

Windows의 C:, D: 드라이브 구조와 달리
Linux는 하나의 디렉터리 계층 아래에
다양한 파일시스템을 마운트하여 사용한다.

### 주요 디렉터리

| 경로 | 역할 |
|---|---|
| `/` | 파일시스템 계층의 시작점 |
| `/home` | 일반 사용자 홈 디렉터리 |
| `/root` | root 관리자 홈 디렉터리 |
| `/etc` | 시스템 및 서비스 설정 |
| `/var/log` | 시스템·애플리케이션 로그 |
| `/usr` | 프로그램·라이브러리 |
| `/opt` | 별도 설치 프로그램 |
| `/tmp` | 임시 파일 |
| `/dev` | 장치 파일 |
| `/proc` | 프로세스·커널 정보 |
| `/sys` | 커널·장치 정보 |
| `/boot` | 부팅 관련 파일 |

### 실무 예시 — Nginx

```text
/etc/nginx/       → 설정 파일
/var/log/nginx/   → 로그 파일
/usr/sbin/nginx   → 실행 파일
/var/www/html/    → 기본 웹 문서 경로 예시
```

**핵심**

- 설정 파일을 찾을 때: `/etc`
- 로그를 확인할 때: `/var/log`
- 사용자 파일을 관리할 때: `/home`

---

# 2. 절대경로와 상대경로

## 2.1 절대경로

루트 디렉터리 `/`부터 시작하는 전체 경로이다.

```text
/home/infra/linux-project/ch02/logs/app.log
```

현재 작업 위치에 관계없이 동일한 경로를 가리킨다.

## 2.2 상대경로

현재 작업 디렉터리를 기준으로 하는 경로이다.

```text
logs/app.log
```

현재 위치가 다음과 같다면:

```text
/home/infra/linux-project/ch02
```

위 상대경로는 다음 파일을 가리킨다.

```text
/home/infra/linux-project/ch02/logs/app.log
```

### 경로 표현

| 표현 | 의미 |
|---|---|
| `/` | 루트 디렉터리 |
| `~` | 사용자 홈 디렉터리 |
| `.` | 현재 디렉터리 |
| `..` | 상위 디렉터리 |
| `cd -` | 이전 작업 디렉터리로 이동 |

**핵심:** 파일을 찾지 못하면 현재 작업 경로를 먼저 확인한다.

---

# 3. 파일·디렉터리 기본 명령어

## 3.1 위치 확인 및 이동

```bash
# 현재 디렉터리 확인
pwd

# 파일 목록 확인
ls

# 상세 목록 확인
ls -l

# 숨김 파일 포함
ls -la

# 파일 크기를 읽기 쉬운 단위로 표시
ls -lh

# 홈 디렉터리 이동
cd ~

# 상위 디렉터리 이동
cd ..

# 이전 디렉터리 이동
cd -
```

### 주요 옵션

| 옵션 | 설명 |
|---|---|
| `ls -l` | 상세 정보 표시 |
| `ls -a` | 숨김 파일 포함 |
| `ls -h` | 사람이 읽기 쉬운 크기 표시 |

`pwd`는 Print Working Directory의 약자이다.

---

## 3.2 디렉터리 및 파일 생성

```bash
# 디렉터리 생성
mkdir test

# 상위 경로까지 함께 생성
mkdir -p project/logs

# 빈 파일 생성
touch test.txt
```

### 옵션 설명

- `mkdir`: 디렉터리 생성
- `-p`: 필요한 상위 디렉터리도 생성
- `touch`: 파일 생성 또는 수정 시각 갱신

---

## 3.3 파일 복사

```bash
# 파일 복사
cp test.txt backup.txt

# 디렉터리 재귀 복사
cp -r project project-backup
```

- `cp`: Copy
- `-r`: 디렉터리와 하위 항목을 재귀적으로 복사

---

## 3.4 파일 이동 및 이름 변경

```bash
# 파일 이름 변경
mv test.txt test2.txt

# 파일 이동
mv test2.txt project/
```

`mv`는 Move의 약자이며,
파일 이동과 이름 변경에 모두 사용한다.

---

## 3.5 파일 삭제

```bash
# 삭제 전 확인
rm -i backup.txt

# 빈 디렉터리 삭제
rmdir test
```

### 주의사항

`rm`으로 삭제한 파일은 일반적인 휴지통으로 이동하지 않는다.

특히 `rm -rf`는 강제 재귀 삭제를 수행하므로
운영 서버에서 사용할 때 매우 주의해야 한다.

---

# 4. 파일 내용 확인 명령어

| 명령어 | 기능 |
|---|---|
| `cat` | 전체 내용 출력 |
| `head` | 파일 앞부분 출력 |
| `tail` | 파일 뒷부분 출력 |
| `less` | 페이지 단위 파일 조회 |
| `wc -l` | 줄 수 계산 |

### 실습

```bash
# 전체 내용 확인
cat logs/app.log

# 처음 3줄 확인
head -n 3 logs/app.log

# 마지막 3줄 확인
tail -n 3 logs/app.log

# 로그 실시간 확인
tail -f logs/app.log

# 총 줄 수 계산
wc -l logs/app.log

# 페이지 단위 확인
less logs/app.log
```

### 주요 옵션

- `-n 3`: 3줄 출력
- `tail -f`: 새로 추가되는 내용을 계속 확인
- `less` 종료: `q`
- `tail -f` 종료: `Ctrl + C`

**실무 활용:** 애플리케이션 장애 발생 시 최근 로그부터 확인한다.

---

# 5. find와 grep

## 5.1 find — 파일 위치 검색

`find`는 파일과 디렉터리를 검색한다.

```bash
# 현재 디렉터리 이하 파일 검색
find . -type f

# .log 파일 검색
find . -type f -name '*.log'

# config 디렉터리 검색
find . -type d -name 'config'
```

### 옵션

| 옵션 | 의미 |
|---|---|
| `.` | 현재 경로부터 검색 |
| `-type f` | 일반 파일 |
| `-type d` | 디렉터리 |
| `-name` | 이름으로 검색 |
| `*.log` | .log로 끝나는 파일명 패턴 |

---

## 5.2 grep — 파일 내용 검색

`grep`은 파일 내부에서 특정 문자열을 검색한다.

```bash
# ERROR 문자열 검색
grep 'ERROR' logs/app.log

# 줄 번호 표시
grep -n 'ERROR' logs/app.log

# 대소문자 무시
grep -i 'error' logs/app.log

# 하위 디렉터리 재귀 검색
grep -Rni 'error' logs/
```

### 옵션

| 옵션 | 의미 |
|---|---|
| `-n` | 줄 번호 출력 |
| `-i` | 대소문자 구분하지 않음 |
| `-R` | 하위 디렉터리 재귀 검색 |

### find와 grep 차이

| 명령어 | 목적 |
|---|---|
| `find` | 파일이 어디에 있는지 검색 |
| `grep` | 파일 내용에 어떤 문자열이 있는지 검색 |

**핵심:** 파일 위치는 `find`, 오류 메시지는 `grep`.

---

# 6. 파이프와 리다이렉션

## 6.1 파이프 (|)

파이프는 앞 명령어의 표준 출력을
다음 명령어의 표준 입력으로 전달한다.

```bash
grep 'ERROR' logs/app.log | wc -l
```

### 동작 과정

```text
grep 'ERROR'
      |
      v
ERROR가 포함된 줄 추출
      |
      v
wc -l
      |
      v
ERROR가 포함된 줄 개수 출력
```

**실무 활용:** 로그에서 오류 발생 건수 계산.

---

## 6.2 리다이렉션

| 기호 | 기능 |
|---|---|
| `>` | 파일 덮어쓰기 |
| `>>` | 파일 끝에 추가 |
| `<` | 파일을 표준 입력으로 사용 |
| `2>` | 표준 오류를 파일에 저장 |
| `|` | 명령어 간 출력·입력 연결 |

### 실습

```bash
# 오류 검색 결과 저장
grep 'ERROR' logs/app.log > backup/errors.txt

# 기존 파일에 내용 추가
echo 'INFO backup completed' >> logs/app.log

# 화면 출력과 파일 저장을 동시에 수행
grep 'ERROR' logs/app.log | tee backup/report.txt
```

### 주의

- `>`: 기존 내용을 덮어쓴다.
- `>>`: 기존 내용 뒤에 추가한다.

---

# 7. printf 명령어

`printf`는 정해진 형식에 따라 문자열을 출력하는 명령어이다.

### 실습용 로그 생성

```bash
printf '%s\n' \
'2026-11-17 INFO application started' \
'2026-11-17 INFO GET /health 200' \
'2026-11-17 ERROR GET /api 500' \
'2026-11-17 WARN disk usage 81%' \
'2026-11-17 ERROR GET /admin 403' > logs/app.log
```

### 구성 요소

| 구성 | 의미 |
|---|---|
| `printf` | 문자열 형식 지정 출력 |
| `%s` | 문자열 출력 |
| `\n` | 줄바꿈 |
| 줄 끝 `\` | 다음 줄로 명령어 연결 |
| `>` | 출력 결과를 파일에 기록 |
| `logs/app.log` | 결과 저장 파일 |

### 생성된 로그

```text
2026-11-17 INFO application started
2026-11-17 INFO GET /health 200
2026-11-17 ERROR GET /api 500
2026-11-17 WARN disk usage 81%
2026-11-17 ERROR GET /admin 403
```

**중요:** 명령어를 여러 줄로 작성할 때,
줄 끝의 `\` 뒤에 불필요한 공백이 있으면
의도대로 줄이 연결되지 않을 수 있다.

---

# 8. 심볼릭 링크와 하드 링크

## 8.1 심볼릭 링크

심볼릭 링크는 다른 파일의 경로를 참조한다.

```bash
ln -s /home/infra/linux-project/ch02/logs/app.log current.log
```

- `ln`: 링크 생성
- `-s`: 심볼릭 링크 생성

원본 경로가 사라지면 링크가 깨질 수 있다.

## 8.2 하드 링크

하드 링크는 동일한 파일의 inode를 참조하는
추가 이름을 생성한다.

```bash
ln logs/app.log app-hardlink.log

# inode 확인
ls -li logs/app.log app-hardlink.log
```

### 차이점

| 구분 | 심볼릭 링크 | 하드 링크 |
|---|---|---|
| 연결 | 경로 참조 | 같은 inode 참조 |
| 원본 이름 삭제 | 깨질 수 있음 | 다른 링크로 접근 가능 |
| 파일시스템 간 연결 | 가능 | 일반적으로 불가능 |
| 명령어 | `ln -s` | `ln` |

---

# 9. tar 압축과 복원

`tar`는 여러 파일을 하나의 아카이브로 묶는다.

`-z` 옵션을 사용하면 gzip 압축도 수행한다.

```bash
# 로그 디렉터리 압축
tar -czf backup/logs.tar.gz logs

# 아카이브 내부 목록
tar -tzf backup/logs.tar.gz

# 압축 해제
tar -xzf backup/logs.tar.gz -C backup

# 원본과 복원 파일 비교
cmp logs/app.log backup/logs/app.log
```

### 옵션

| 옵션 | 의미 |
|---|---|
| `-c` | 아카이브 생성 |
| `-x` | 아카이브 추출 |
| `-t` | 내부 파일 목록 |
| `-z` | gzip 압축·해제 |
| `-f` | 아카이브 파일 지정 |
| `-C` | 대상 디렉터리 지정 |

**실무 활용:** 로그 및 설정 파일 백업과 복원.

---

# 10. 종합 실습 — 운영 로그 분석

## 10.1 실습 디렉터리 생성

```bash
mkdir -p ~/linux-project/ch02/{logs,config,backup}

cd ~/linux-project/ch02

pwd
ls -la
```

### 디렉터리 구조

```text
linux-project/
└── ch02/
    ├── logs/
    ├── config/
    └── backup/
```

## 10.2 애플리케이션 로그 생성

```bash
printf '%s\n' \
'2026-11-17 INFO application started' \
'2026-11-17 INFO GET /health 200' \
'2026-11-17 ERROR GET /api 500' \
'2026-11-17 WARN disk usage 81%' \
'2026-11-17 ERROR GET /admin 403' > logs/app.log
```

## 10.3 장애 로그 분석

```bash
# 로그 위치 검색
find . -type f -name 'app.log'

# ERROR 검색
grep -n 'ERROR' logs/app.log

# ERROR 건수 확인
grep 'ERROR' logs/app.log | wc -l

# ERROR만 파일에 저장
grep 'ERROR' logs/app.log > backup/errors.txt

# 저장 결과 확인
cat backup/errors.txt
```

### 예상 결과

```text
2026-11-17 ERROR GET /api 500
2026-11-17 ERROR GET /admin 403
```

ERROR가 포함된 줄: 2개

## 10.4 로그 백업

```bash
tar -czf backup/logs.tar.gz logs

tar -tzf backup/logs.tar.gz

tar -xzf backup/logs.tar.gz -C backup

cmp logs/app.log backup/logs/app.log
```

### 검증

- ERROR 검색 결과가 정확한가?
- ERROR 줄 개수가 2개인가?
- 백업 파일이 생성되었는가?
- 압축 해제 후 파일 내용이 동일한가?

---

# 11. 장애 대응

## 장애 1. 파일이 존재하지 않는다는 오류

```text
No such file or directory
```

### 원인

- 현재 경로가 다름
- 파일명 오타
- 파일이 이동되거나 삭제됨

### 대응

```bash
pwd

ls -la

find . -type f -name 'app.log'

cat logs/app.log
```

---

## 장애 2. Permission denied

### 원인 후보

- 사용자에게 읽기·쓰기 권한 없음
- 상위 디렉터리 접근 권한 없음
- 파일 소유자·그룹 설정 문제

### 점검

```bash
whoami

id

ls -l logs/app.log

ls -ld logs
```

권한 변경은 필요한 범위만 적용한다.

무조건 `chmod 777`을 사용하지 않는다.

---

## 장애 3. 디스크 공간 부족

### 점검

```bash
# 파일시스템 사용량
df -h

# 특정 디렉터리 사용량
du -sh ~/linux-project
```

- `df`: 파일시스템의 공간 사용량 확인
- `du`: 파일·디렉터리의 공간 사용량 확인
- `-h`: 읽기 쉬운 단위로 표시
- `-s`: 합계만 출력

---

# 12. 면접 예상 질문

### Q1. Linux의 /etc와 /var/log는 무엇인가요?

`/etc`는 시스템 및 서비스 설정 파일을,
`/var/log`는 각종 로그를 저장하는 데 사용하는
대표적인 디렉터리입니다.

### Q2. 절대경로와 상대경로의 차이는?

절대경로는 `/`부터 시작하는 전체 경로이고,
상대경로는 현재 작업 디렉터리를 기준으로 합니다.

### Q3. find와 grep의 차이는?

`find`는 파일 및 디렉터리의 위치를 검색하고,
`grep`은 파일 내부의 특정 문자열을 검색합니다.

### Q4. 파이프와 리다이렉션의 차이는?

파이프는 명령어의 출력을 다음 명령어의
입력으로 전달합니다.

리다이렉션은 명령어의 입출력을
파일 등 다른 대상으로 연결합니다.

### Q5. Linux 서버에서 오류 로그를 분석하는 방법은?

먼저 로그 경로를 확인하고,
`tail` 또는 `less`로 로그를 조회합니다.

이후 `grep`으로 오류를 검색하고,
오류 발생 시각과 관련 기록을 비교하여
장애 원인을 좁혀갑니다.

---

# 13. 핵심 명령어 요약

| 명령어 | 역할 |
|---|---|
| `pwd` | 현재 위치 |
| `ls` | 파일 목록 |
| `cd` | 디렉터리 이동 |
| `mkdir` | 디렉터리 생성 |
| `touch` | 빈 파일 생성 |
| `cp` | 복사 |
| `mv` | 이동·이름 변경 |
| `rm` | 삭제 |
| `cat` | 파일 전체 조회 |
| `head` | 앞부분 조회 |
| `tail` | 뒷부분 조회 |
| `less` | 페이지 단위 조회 |
| `find` | 파일 위치 검색 |
| `grep` | 문자열 검색 |
| `wc -l` | 줄 수 계산 |
| `tee` | 화면 출력 및 파일 저장 |
| `ln` | 링크 생성 |
| `tar` | 아카이브·압축 |
| `df` | 파일시스템 사용량 |
| `du` | 디렉터리 사용량 |

---

# 14. 학습 완료 체크리스트

- [ ] 주요 Linux 디렉터리 역할 이해
- [ ] 절대경로와 상대경로 이해
- [ ] 파일 생성·복사·이동·삭제 실습
- [ ] `cat`, `head`, `tail`, `less` 사용
- [ ] `find`와 `grep` 차이 이해
- [ ] 파이프·리다이렉션 실습
- [ ] 심볼릭 링크·하드 링크 개념 이해
- [ ] `tar` 압축·복원 실습
- [ ] ERROR 로그 검색 및 결과 저장
- [ ] 파일 관련 장애 대응 실습

---

## 최종 핵심

Linux 서버 관리에서 가장 기본적인 작업은 다음과 같다.

```text
1. 파일 위치 확인
        ↓
2. 파일 내용 조회
        ↓
3. 필요한 내용 검색
        ↓
4. 결과 가공 및 저장
        ↓
5. 백업 및 검증
        ↓
6. 장애 원인 분석
```

**학습 목표: Linux 서버에서 필요한 파일을
스스로 찾고, 설정 및 로그를 관리하며,
기본적인 파일 관련 장애를 분석할 수 있다.**

---

## 다음 학습

**3장 1교시 — Linux 사용자·그룹·권한·sudo·ACL 관리**
