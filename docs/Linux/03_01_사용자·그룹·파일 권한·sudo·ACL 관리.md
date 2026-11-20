<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/4bd920b2-780a-44b0-b500-be68fb982177" />

# Linux 프로젝트 — 3장 1교시
## 사용자·그룹·파일 권한·sudo·ACL 관리

### 1. 사용자와 그룹

Linux는 UID와 GID를 이용해 사용자와 그룹을 식별한다.

| 개념 | 설명 |
|---|---|
| User | Linux 사용자 계정 |
| UID | 사용자 식별 번호 (root = 0) |
| Group | 여러 사용자에게 공통 권한 적용 |
| GID | 그룹 식별 번호 |

```bash
whoami                      # 현재 사용자 확인
id                          # UID, GID, 그룹 확인
sudo useradd -m ops01       # 사용자 생성
sudo groupadd appops        # 그룹 생성
sudo usermod -aG appops ops01  # 기존 보조 그룹 유지하며 추가
```

### 2. 파일 권한 (rwx)

Linux 파일 권한은 **Owner / Group / Others**로 구분한다.

| 권한 | 숫자 | 의미 |
|---|---|---|
| r | 4 | 읽기 |
| w | 2 | 쓰기 |
| x | 1 | 실행 |

**대표적인 권한**

| 권한 | 의미 |
|---|---|
| 644 | 소유자 rw / 그룹 r / Others r |
| 640 | 소유자 rw / 그룹 r / Others 없음 |
| 755 | 소유자 rwx / 그룹 rx / Others rx |
| 700 | 소유자만 rwx |

※ 디렉터리에서 `x`는 경로 통과 권한이다.

### 3. chmod · chown · chgrp

```bash
chmod 640 app.conf                 # 접근 권한 변경
sudo chown infra:appops app.conf   # 소유자·그룹 변경
sudo chgrp appops app.conf         # 그룹 변경
ls -l app.conf                     # 파일 권한 확인
```

- `chmod`: 권한 변경
- `chown`: 소유자·그룹 변경
- `chgrp`: 소유 그룹 변경

### 4. sudo

`sudo`는 허용된 사용자가 다른 사용자(기본 root)의 권한으로 명령어를 실행하는 기능이다.

```bash
sudo apt update    # 관리자 권한 실행
sudo -l            # sudo 사용 가능 명령 확인
sudo visudo -c     # sudoers 문법 검사
```

**핵심:** 필요한 권한만 부여하는 최소 권한 원칙을 적용한다.

### 5. ACL (Access Control List)

기본 rwx 권한 외에 특정 사용자나 그룹에 개별 권한을 설정하는 기능이다.

```bash
# audit01에게 읽기 권한 부여
sudo setfacl -m u:audit01:r-- app.conf

# ACL 확인
getfacl app.conf

# ACL 항목 제거
sudo setfacl -x u:audit01 app.conf
```

※ 파일에 읽기 권한이 있어도 상위 디렉터리의 `x` 권한이 없으면 접근할 수 없다.

### 6. Permission denied 장애 대응

```bash
whoami                 # 현재 사용자
id                     # 사용자·그룹 확인
ls -l app.conf         # 파일 소유권·권한 확인
namei -l /경로/app.conf # 상위 디렉터리 권한 확인
getfacl app.conf       # ACL 확인
```

**장애 분석 순서**

1. 사용자·그룹 확인
2. 파일 소유자와 rwx 권한 확인
3. 상위 디렉터리 접근 권한 확인
4. ACL 설정 확인
5. 최소 권한으로 수정 후 재검증

### 7. 핵심 요약

| 명령어 | 역할 |
|---|---|
| `id` | UID·GID·그룹 조회 |
| `useradd` | 사용자 생성 |
| `usermod` | 사용자·그룹 정보 수정 |
| `chmod` | 파일 권한 변경 |
| `chown` | 소유자 변경 |
| `sudo` | 관리자 권한 실행 |
| `setfacl` | ACL 설정 |
| `getfacl` | ACL 확인 |
| `namei -l` | 경로별 권한 분석 |

### 면접 핵심 질문

**Q. chmod와 chown의 차이는?**

- chmod: 파일 접근 권한 변경
- chown: 파일 소유자 및 그룹 변경

**Q. ACL은 왜 사용하나요?**

- Owner / Group / Others의 기본 권한만으로 부족할 때 특정 사용자에게 별도 권한을 부여하기 위해 사용한다.

**Q. Permission denied 발생 시 어떻게 대응하나요?**

- 사용자·그룹 → 파일 권한 → 상위 디렉터리 권한 → ACL 순서로 원인을 분석한다.

---

**최종 핵심:** Linux 서버에서는 사용자와 그룹을 기준으로 파일 접근을 통제하며, `chmod`, `chown`, `ACL`을 활용해 최소 권한 원칙을 적용한다.
