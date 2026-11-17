



# Windows OS 프로젝트식 학습
## 1장 3교시 — 사용자·그룹·권한·UAC·Registry

### 학습 목표
1. Windows 사용자와 그룹의 역할 이해
2. 인증(Authentication)과 인가(Authorization)의 차이 이해
3. 일반 사용자와 관리자 권한의 차이 이해
4. UAC의 역할과 필요성 이해
5. Registry의 기본 구조 이해
6. 사용자·그룹·권한 관리 명령어 학습

---

## 1. 사용자 계정(User)

사용자 계정은 Windows가 사용자를 식별하고 로그인 및 접근 권한을 관리하기 위한 기본 단위이다.

### 계정 종류

| 구분 | 로컬 계정 | 도메인 계정 |
|---|---|---|
| 관리 위치 | 개별 Windows PC | Active Directory |
| 계정 관리 | 해당 컴퓨터 | 중앙 관리 |
| 주요 용도 | 개인 PC, 독립 서버 | 기업 인프라 |

예시:
- 로컬 계정: WIN01\rdpuser
- 도메인 계정: COMPANY\user01

**핵심:** 로컬 계정은 개별 컴퓨터에서 관리하고, 도메인 계정은 Active Directory에서 중앙 관리한다.

---

## 2. 인증과 인가

### 인증(Authentication)
사용자가 누구인지 확인하는 과정이다.

예시:
- 사용자 이름 입력
- 비밀번호 확인
- 로그인 성공

### 인가(Authorization)
인증된 사용자가 특정 작업을 수행할 권한이 있는지 확인하는 과정이다.

예시:
- RDP 접속 권한 확인
- 특정 폴더 접근 권한 확인
- 관리자 작업 수행 권한 확인

### 실제 RDP 접속 과정

1. rdpuser 계정 생성
2. Remote Desktop Users 그룹에 추가
3. MobaXterm에서 계정과 암호 입력
4. Windows가 사용자 인증
5. Windows가 원격 로그온 권한 확인
6. 권한이 허용되면 RDP 접속 성공

**핵심**

인증 = 너는 누구인가?

인가 = 너는 이 작업을 해도 되는가?

※ 암호가 맞아도 원격 로그온 권한이 없다면 접속이 거부될 수 있다.

---

## 3. 그룹(Group)

그룹은 여러 사용자에게 공통된 권한을 효율적으로 부여하기 위한 기능이다.

### 그룹이 필요한 이유

직원 20명에게 각각 파일 권한을 설정하는 것보다 그룹에 권한을 부여하고 사용자를 그룹에 추가하는 방식이 관리하기 쉽다.

### 대표적인 Windows 그룹

| 그룹 | 역할 |
|---|---|
| Administrators | 시스템 관리 권한 |
| Users | 일반 사용자 그룹 |
| Remote Desktop Users | 원격 데스크톱 로그온 권한 |
| Backup Operators | 백업·복원 관련 권한 |

### 최소 권한 원칙(Least Privilege)

사용자에게 업무에 필요한 최소한의 권한만 부여하는 보안 원칙이다.

예시:
- rdpuser는 원격 접속이 목적
- Remote Desktop Users 그룹에 추가
- 불필요한 Administrators 권한은 부여하지 않음

**핵심:** 사용자마다 권한을 직접 관리하기보다 그룹 기반으로 관리하고 필요한 최소 권한만 부여한다.

---

## 4. 일반 사용자와 관리자

### 일반 사용자(Standard User)
- 일반 프로그램 실행
- 본인 파일 관리
- 시스템 설정 변경에 제한 존재

### 관리자(Administrator)
- 사용자 및 그룹 관리
- 시스템 설정 변경
- 서비스 구성 관리
- 관리자 권한이 필요한 작업 수행

관리자 그룹에 속해 있더라도 UAC에 의해 일반 작업은 제한된 권한으로 실행될 수 있다.

---

## 5. UAC(User Account Control)

UAC는 관리자 권한이 필요한 작업을 수행할 때 승인 또는 관리자 자격 증명을 요구하는 Windows 보안 기능이다.

### 등장 배경

모든 프로그램을 항상 관리자 권한으로 실행하면 악성 프로그램이나 실수로 시스템 설정이 변경될 위험이 커진다.

### 동작 원리

일반 사용자
   ↓
관리자 권한이 필요한 작업 실행
   ↓
UAC 창 표시
   ↓
관리자 자격 증명 입력
   ↓
권한 상승 승인
   ↓
관리자 권한으로 작업 실행

### 핵심 특징

- 관리자 권한 상승을 통제한다.
- 표준 사용자는 관리자 자격 증명이 필요할 수 있다.
- 관리자 계정에도 승인 창이 표시될 수 있다.
- UAC는 백신 프로그램이 아니다.

### Linux와 비교

| Windows | Linux |
|---|---|
| 일반 사용자 | 일반 사용자 |
| Administrators | sudo/wheel 그룹 등 |
| UAC 권한 상승 | sudo 등을 통한 권한 상승 |

※ UAC와 sudo는 동일한 기술은 아니지만 권한 상승을 이해할 때 비교할 수 있다.

---

## 6. ACL과 파일 접근 권한

ACL(Access Control List)은 사용자 또는 그룹이 파일과 폴더에 접근할 수 있는 권한을 정의하는 목록이다.

### 대표적인 NTFS 권한

| 권한 | 의미 |
|---|---|
| Read | 파일 읽기 |
| Write | 파일 쓰기 |
| Read & Execute | 읽기 및 실행 |
| Modify | 읽기·쓰기·수정·삭제 등 |
| Full Control | 모든 권한 및 권한 변경 등 |

실제 접근 가능 여부는 사용자·그룹 권한, 상속, 거부 규칙 등에 따라 결정된다.

**핵심:** 인증에 성공하더라도 해당 파일에 접근할 권한이 없으면 접근이 거부될 수 있다.

---

## 7. Registry(레지스트리)

Registry는 Windows와 여러 응용 프로그램의 설정 정보를 저장하는 계층형 데이터베이스이다.

### 주요 영역

| Registry | 역할 |
|---|---|
| HKEY_LOCAL_MACHINE | 컴퓨터 전체 관련 설정 |
| HKEY_CURRENT_USER | 현재 사용자 관련 설정 |
| HKEY_USERS | 로드된 사용자 프로필 설정 |
| HKEY_CLASSES_ROOT | 파일 연결 및 프로그램 등록 정보 등 |

### Registry 구조

HKEY_CURRENT_USER
 └── Software
      └── WindowsOS_Lesson13
           └── LessonStatus = Practice

### Registry 관리 시 주의사항
1. 변경 대상과 영향을 먼저 확인한다.
2. 변경 전에 백업한다.
3. 필요한 설정만 수정한다.
4. 변경 후 정상 동작을 검증한다.

**핵심:** Registry는 Windows 설정 저장소이며 잘못 수정하면 시스템 장애가 발생할 수 있다.

---

## 8. PowerShell 핵심 명령어

### 현재 사용자 확인

```powershell
whoami
```

### 로컬 계정 조회

```powershell
Get-LocalUser
```

### 특정 계정 조회

```powershell
Get-LocalUser -Name rdpuser
```

### 로컬 그룹 조회

```powershell
Get-LocalGroup
```

### RDP 사용자 그룹 조회

```powershell
$rdpGroup = Get-LocalGroup -SID 'S-1-5-32-555'
Get-LocalGroupMember -Group $rdpGroup
```

S-1-5-32-555는 기본 Remote Desktop Users 그룹의 SID이다.

### 사용자 소속 그룹 확인

```powershell
whoami /groups
```

### 학습용 그룹 생성
관리자 PowerShell에서 실행:

```powershell
New-LocalGroup -Name "WinOSLab"
```

### 그룹에 사용자 추가

```powershell
Add-LocalGroupMember -Group "WinOSLab" -Member "rdpuser"
```

### 그룹 구성원 확인

```powershell
Get-LocalGroupMember -Group "WinOSLab"
```

### 폴더 ACL 확인

```powershell
Get-Acl "$env:USERPROFILE" |
    Format-List Owner, AccessToString
```

### Registry 조회

```powershell
Get-ItemProperty -Path "HKCU:\Software"
```

### GUI 관리 도구

| 명령어 | 역할 |
|---|---|
| lusrmgr.msc | 로컬 사용자·그룹 관리 |
| regedit | Registry 편집기 |
| secpol.msc | 로컬 보안 정책 |
| SystemPropertiesRemote | 원격 접속 관련 시스템 설정 |

---

## 9. 실무 장애 대응

### 상황 1. RDP 로그인이 거부됨

확인 항목:
1. 사용자 계정 존재 여부
2. 계정 활성화 상태
3. 사용자 이름 및 암호
4. Remote Desktop Users 그룹
5. 원격 로그온 정책
6. RDP 서비스 및 네트워크 상태

### 상황 2. 관리자 권한이 없다는 오류

확인 항목:
1. 현재 로그인 사용자
2. 관리자 그룹 소속 여부
3. 작업에 필요한 권한
4. UAC 권한 상승 여부

### 상황 3. 폴더 접근 거부

확인 항목:
1. 파일 및 폴더 ACL
2. 사용자·그룹 멤버십
3. 권한 상속 여부
4. 명시적인 거부 권한 존재 여부

### 상황 4. Registry 변경 후 오류 발생

대응 절차:
1. 최근 변경 내역 확인
2. 관련 설정과 오류 로그 확인
3. 백업 및 복원 방법 검토
4. 승인된 변경 복구
5. 정상 동작 재검증

---

## 10. 기술면접 예상 질문

### Q1. 사용자와 그룹의 차이는 무엇인가요?

사용자는 개별 계정을 의미하고, 그룹은 여러 사용자에게 공통 권한을 효율적으로 부여하기 위한 기능입니다.

### Q2. 인증과 인가의 차이는 무엇인가요?

인증은 사용자의 신원을 확인하는 과정이며, 인가는 인증된 사용자가 특정 자원이나 작업에 접근할 권한이 있는지 확인하는 과정입니다.

### Q3. UAC란 무엇인가요?

UAC는 관리자 권한이 필요한 작업을 수행할 때 승인이나 관리자 자격 증명을 요구하는 보안 기능입니다.

### Q4. 최소 권한 원칙이란 무엇인가요?

사용자가 업무를 수행하는 데 필요한 최소한의 권한만 부여하는 보안 원칙입니다.

### Q5. Registry란 무엇인가요?

Registry는 Windows와 응용 프로그램의 설정 정보를 저장하는 계층형 데이터베이스입니다.

---

## 11. 최종 핵심 암기

| 개념 | 핵심 내용 |
|---|---|
| User | Windows 사용자 계정 |
| Local User | 개별 컴퓨터에서 관리하는 계정 |
| Domain User | Active Directory에서 관리하는 계정 |
| Group | 여러 사용자에 대한 공통 권한 관리 |
| Authentication | 사용자 신원 확인 |
| Authorization | 접근 및 작업 권한 확인 |
| Administrator | 시스템 관리 권한 |
| Least Privilege | 필요한 최소 권한만 부여 |
| UAC | 관리자 권한 상승 통제 |
| ACL | 파일·폴더 등의 접근 권한 목록 |
| SID | Windows 보안 주체의 식별자 |
| Registry | Windows 및 프로그램 설정 데이터베이스 |

### 최종 요약

1. Windows는 사용자 계정을 통해 사용자를 식별한다.
2. 인증은 신원 확인이고 인가는 권한 확인이다.
3. 그룹을 활용하면 여러 사용자의 권한을 효율적으로 관리할 수 있다.
4. 업무에 필요한 최소한의 권한만 부여해야 한다.
5. UAC는 관리자 권한 상승을 통제하는 기능이다.
6. ACL은 사용자와 그룹의 파일 접근 권한을 관리한다.
7. Registry는 Windows와 프로그램 설정 정보를 저장한다.

**1장 3교시 핵심 학습 범위 정리 완료**
