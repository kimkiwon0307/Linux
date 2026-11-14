<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/c15baf36-e9db-4aea-96b2-ef0f898348a4" />



# Windows OS 프로젝트식 학습
## 1장 2교시 — Windows 설치, 부팅 구조, NTFS 및 디스크 관리

### 학습 목표
1. Windows 설치 과정과 ISO 파일의 역할 이해
2. BIOS, UEFI, GPT, MBR 개념 이해
3. Windows 부팅 과정 이해
4. NTFS 파일 시스템의 특징 이해
5. 디스크, 파티션, 볼륨 차이 이해
6. VMware에 Windows 11 설치 및 검증

---

## 1. Windows 설치와 ISO

### ISO 파일이란?
ISO는 운영체제 설치 미디어의 내용을 하나의 파일로 저장한 디스크 이미지이다.

Windows와 Linux 모두 ISO 파일을 이용해 운영체제를 설치할 수 있다.

### 설치 과정

1. Windows 11 ISO 다운로드
2. VMware 가상 머신 생성
3. CPU, RAM, 가상 디스크 설정
4. UEFI, Secure Boot, TPM 설정
5. ISO 연결 및 VM 실행
6. Windows 11 Pro 설치
7. Windows 초기 설정
8. 설치 후 정상 동작 검증

### 실습 환경

| 항목 | 설정 |
|---|---|
| 가상화 | VMware Workstation Pro 17 |
| OS | Windows 11 Pro |
| CPU | 2 vCPU |
| RAM | 8GB |
| Disk | 80GB |
| Firmware | UEFI |
| TPM | vTPM 2.0 |
| Partition Style | GPT |
| File System | NTFS |

---

## 2. BIOS와 UEFI

BIOS와 UEFI는 컴퓨터 전원이 켜질 때 하드웨어를 초기화하고 운영체제 부팅을 준비하는 펌웨어 방식이다.

### BIOS (Basic Input/Output System)
- 오래된 펌웨어 방식
- Legacy 부팅 환경에서 사용
- 일반적으로 MBR 파티션 방식과 함께 사용

### UEFI (Unified Extensible Firmware Interface)
- 현대적인 펌웨어 인터페이스
- 일반적으로 GPT와 함께 사용
- Secure Boot 기능 지원
- EFI 부팅 프로그램을 통해 OS 부팅

### BIOS와 UEFI 비교

| 구분 | Legacy BIOS | UEFI |
|---|---|---|
| 부팅 방식 | 기존 BIOS 방식 | EFI 부팅 프로그램 |
| 일반적인 파티션 방식 | MBR | GPT |
| Secure Boot | 미지원 | 지원 |
| Windows 11 | 공식 요구 사항에 부적합 | 공식 요구 사항 |

**핵심:** UEFI는 운영체제를 부팅하기 위한 펌웨어 인터페이스이다.

---

## 3. GPT와 MBR

GPT와 MBR은 디스크의 파티션 구성 정보를 관리하는 방식이다.

### MBR (Master Boot Record)
- 오래된 파티션 테이블 방식
- 일반적인 512바이트 섹터 구성에서 약 2TiB 용량 제한
- 기본 파티션 최대 4개

### GPT (GUID Partition Table)
- 현대적인 파티션 테이블 방식
- 대용량 디스크 지원
- 여러 파티션 구성 가능
- Windows UEFI 부팅에 일반적으로 사용

### GPT와 MBR 비교

| 구분 | MBR | GPT |
|---|---|---|
| 방식 | 기존 파티션 테이블 | 현대적인 파티션 테이블 |
| 용량 | 일반적으로 약 2TiB 한계 | 대용량 지원 |
| 파티션 수 | 기본 파티션 최대 4개 | Windows에서 일반적으로 최대 128개 |
| Windows UEFI 부팅 | 일반적으로 사용하지 않음 | 사용 |

**주의**

UEFI와 GPT는 서로 다른 개념이다.

- UEFI: 부팅을 담당하는 펌웨어 인터페이스
- GPT: 디스크 파티션 구성 방식
- NTFS: 파일을 저장하고 관리하는 파일 시스템

---

## 4. Windows 부팅 과정

Windows는 컴퓨터 전원을 켜면 여러 단계를 거쳐 실행된다.

### UEFI 환경의 Windows 부팅 순서

전원 ON
   ↓
UEFI 펌웨어
   ↓
Windows Boot Manager
   ↓
Windows OS Loader
   ↓
Windows Kernel
   ↓
시스템 서비스 초기화
   ↓
로그인 및 Windows 실행

### 주요 구성 요소

| 구성 요소 | 역할 |
|---|---|
| UEFI | 하드웨어 초기화 및 부팅 시작 |
| bootmgfw.efi | Windows Boot Manager |
| BCD | Windows 부팅 설정 정보 |
| winload.efi | Windows OS Loader |
| ntoskrnl.exe | Windows NT 커널 |

### 핵심 원리

1. UEFI가 하드웨어 초기화
2. Windows Boot Manager 실행
3. BCD를 참조하여 부팅 설정 확인
4. Windows OS Loader가 커널 로딩 준비
5. Windows Kernel 초기화
6. 시스템 서비스가 시작되고 로그인 가능

**핵심:** 부팅 장애가 발생하면 어느 단계에서 문제가 발생했는지 확인해야 한다.

---

## 5. NTFS 파일 시스템

### 파일 시스템이란?

저장장치에 파일을 저장하고 관리하는 구조와 규칙이다.

파일 이름, 위치, 크기, 접근 권한 등을 관리한다.

### NTFS (New Technology File System)

Windows에서 널리 사용하는 파일 시스템이다.

### NTFS 주요 특징

**① 파일 및 폴더 권한 관리**
- ACL(Access Control List) 지원
- 사용자와 그룹별 권한 설정 가능
- 읽기, 쓰기, 수정, 모든 권한 등 관리

**② 저널링(Journaling)**
- 파일 시스템의 메타데이터 변경 기록
- 비정상 종료 이후 일관성 복구 지원
- 파일 내용 전체의 복구를 보장하지는 않음

**③ 대용량 파일 지원**
- FAT32의 단일 파일 약 4GiB 제한이 없음
- 대용량 파일 저장 가능

### 파일 시스템 비교

| 파일 시스템 | 주요 특징 |
|---|---|
| NTFS | Windows 권한 관리, 저널링 |
| FAT32 | 호환성 우수, 파일 크기 제한 |
| exFAT | 이동식 저장장치, 대용량 파일 |
| ext4 | Linux에서 널리 사용 |
| XFS | Linux 서버 및 대용량 파일 시스템 |

---

## 6. 디스크, 파티션, 볼륨

### Disk (디스크)
데이터를 저장하는 물리적 또는 가상 저장장치

예시:
- SSD
- HDD
- VMware 가상 디스크

### Partition (파티션)
디스크를 논리적으로 나눈 영역

### Volume (볼륨)
파일을 저장하고 접근할 수 있도록 구성된 논리적 저장 공간

### 기본 구조

Disk 0 (80GB)
 ├── EFI System Partition
 ├── MSR Partition
 ├── Windows Partition (C:)
 └── Recovery Partition

### Windows 주요 파티션

| 파티션 | 역할 |
|---|---|
| EFI System | 부팅 프로그램 저장 |
| MSR | Microsoft 예약 영역 |
| Windows (C:) | OS 및 프로그램 저장 |
| Recovery | Windows 복구 환경 저장 |

※ 실제 구성과 파티션 크기는 설치 환경에 따라 다를 수 있다.

**주의:** EFI, MSR, Recovery 파티션은 임의로 삭제하지 않는다.

---

## 7. TPM 2.0과 Secure Boot

### TPM (Trusted Platform Module)

암호화 키 등 보안 관련 정보를 보호하는 데 사용하는 보안 기술이다.

Windows 11은 TPM 2.0 지원을 요구한다.

### VMware의 vTPM

가상 머신에서 TPM 기능을 제공하는 가상 장치이다.

VMware Workstation Pro 17에서는 TPM 지원을 위해 VM 암호화 및 UEFI 설정이 필요할 수 있다.

### Secure Boot

부팅 과정에서 부팅 구성 요소의 서명과 허용 정책을 검증하는 UEFI 보안 기능이다.

### VMware TPM 설정 과정

1. 가상 머신 완전히 종료
2. VM Settings → Options → Access Control
3. TPM 지원을 위한 VM 암호화
4. Options → Advanced → UEFI 확인
5. Secure Boot 설정
6. Hardware → Add
7. Trusted Platform Module 추가

---

## 8. Windows 설치 후 검증 명령어

### ① Windows 버전 확인

실행 창:

winver

Windows 11 Pro 설치 여부 확인

### ② UEFI 부팅 확인

실행 창:

msinfo32

확인 항목:
- OS 이름
- BIOS 모드
- 보안 부팅 상태

### ③ TPM 2.0 확인

실행 창:

tpm.msc

확인 항목:
- TPM 사용 준비 상태
- 사양 버전 2.0

### ④ 디스크 확인

```powershell
Get-Disk
```

주요 출력:
- Number: 디스크 번호
- FriendlyName: 디스크 이름
- PartitionStyle: GPT 또는 MBR
- Size: 디스크 크기

### ⑤ 파티션 확인

```powershell
Get-Partition
```

C: 파티션만 확인:

```powershell
Get-Partition -DriveLetter C
```

### ⑥ 파일 시스템 확인

```powershell
Get-Volume
```

C: 드라이브 확인:

```powershell
Get-Volume -DriveLetter C
```

주요 출력:
- DriveLetter: 드라이브 문자
- FileSystem: 파일 시스템 종류
- HealthStatus: 볼륨 상태

### ⑦ 디스크 관리 GUI

실행 창:

diskmgmt.msc

디스크, 파티션, 볼륨 상태 확인 가능

---

## 9. Windows와 Linux 명령어 비교

| 목적 | Windows | Linux |
|---|---|---|
| 디스크 확인 | Get-Disk | lsblk |
| 파티션 확인 | Get-Partition | lsblk, fdisk -l |
| 볼륨 확인 | Get-Volume | lsblk -f |
| 파일 시스템 용량 | Get-Volume | df -h |
| 파일 권한 확인 | Get-Acl | ls -l, getfacl |
| 부팅 설정 확인 | msinfo32, bcdedit | bootctl, efibootmgr 등 |

※ 명령어들이 완전히 동일한 기능을 수행하는 것은 아니다.

---

## 10. VMware Tools와 스냅샷

### VMware Tools

가상 머신과 VMware 환경의 통합 기능을 지원한다.

주요 기능:
- 화면 해상도 조정 지원
- 마우스 사용 편의성 향상
- 호스트와 게스트 간 통합 기능
- 가상 머신 관리 기능 개선

### Snapshot (스냅샷)

특정 시점의 가상 머신 상태를 저장하는 기능이다.

실습 중 문제가 발생했을 때 이전 상태로 되돌릴 수 있다.

스냅샷 이름:

WIN11-Clean-Install

**주의:** 스냅샷은 별도의 백업을 완전히 대체하지 않는다.

---

## 11. 실무 장애 대응

### Q1. Windows에서 No bootable device 오류가 발생한다면?

가능한 원인:
- 부팅 디스크 미인식
- 부팅 순서 오류
- EFI 파티션 문제
- 부팅 파일 손상

확인 절차:
1. UEFI에서 디스크 인식 확인
2. 부팅 순서 확인
3. EFI 파티션과 부팅 파일 상태 확인
4. Windows 복구 환경 이용

### Q2. Windows 11 설치 중 TPM 2.0 오류가 발생한다면?

확인 절차:
1. VMware 가상 머신 종료
2. UEFI 설정 확인
3. VM 암호화 설정 확인
4. vTPM 추가 여부 확인
5. VM 재실행 후 설치 진행

### Q3. Windows에서 디스크 용량 부족 장애가 발생한다면?

확인 절차:
1. 디스크 용량 확인
2. 로그 및 임시 파일 사용량 확인
3. 불필요한 파일 정리
4. 필요하면 디스크 확장 검토
5. 조치 후 사용량 재확인

---

## 12. 기술면접 예상 질문

### Q1. BIOS와 UEFI의 차이는 무엇인가요?

BIOS는 기존의 펌웨어 방식이고 UEFI는 현대적인 펌웨어 인터페이스입니다. UEFI는 GPT 기반 부팅과 Secure Boot 등을 지원합니다.

### Q2. GPT와 MBR의 차이는 무엇인가요?

GPT와 MBR은 디스크 파티션 구성 방식입니다. GPT는 MBR보다 대용량 디스크와 많은 파티션을 지원합니다.

### Q3. NTFS란 무엇인가요?

NTFS는 Windows에서 주로 사용하는 파일 시스템으로 ACL 기반 파일 권한 관리와 저널링 등의 기능을 지원합니다.

### Q4. TPM 2.0은 무엇인가요?

TPM은 암호화 키와 같은 보안 정보를 보호하는 데 사용되는 기술입니다. Windows 11에서는 TPM 2.0 지원이 필요합니다.

### Q5. Windows가 부팅되지 않으면 어떻게 대응하나요?

먼저 오류 메시지와 디스크 인식 상태를 확인하고, UEFI 부팅 순서, EFI 파티션 및 BCD 설정 등을 점검하겠습니다. 필요한 경우 Windows 복구 환경을 이용하겠습니다.

---

## 13. 실제 실습 완료 내역

환경: VMware Workstation Pro 17

- [x] Windows 11 Pro 설치
- [x] UEFI 부팅 확인
- [x] TPM 2.0 확인
- [x] GPT 디스크 확인
- [x] NTFS 파일 시스템 확인
- [x] VMware Tools 설치
- [x] VMware 스냅샷 생성

※ Secure Boot 활성화 여부는 별도 검증 결과 기록 필요

---

## 14. 최종 핵심 암기

| 개념 | 핵심 내용 |
|---|---|
| ISO | 운영체제 설치 이미지 |
| BIOS | 기존 펌웨어 방식 |
| UEFI | 현대적인 부팅 펌웨어 인터페이스 |
| GPT | 디스크 파티션 구성 방식 |
| MBR | 기존 디스크 파티션 구성 방식 |
| Boot Manager | Windows 부팅 관리 |
| BCD | Windows 부팅 설정 정보 |
| NTFS | Windows 파일 시스템 |
| ACL | 파일·폴더 접근 권한 관리 |
| Disk | 물리적 또는 가상 저장장치 |
| Partition | 디스크를 나눈 영역 |
| Volume | 데이터를 저장하는 논리적 공간 |
| TPM | 보안 키 등의 보호에 사용 |
| VMware Tools | 가상 머신 통합 기능 지원 |
| Snapshot | VM 특정 시점 상태 저장 |

### 1장 2교시 최종 요약

1. Windows는 ISO 파일을 이용하여 설치할 수 있다.
2. UEFI는 부팅 펌웨어이고 GPT는 파티션 구성 방식이다.
3. Windows는 Boot Manager와 OS Loader를 거쳐 커널을 실행한다.
4. NTFS는 ACL 기반 접근 권한 관리와 저널링을 지원한다.
5. 디스크, 파티션, 볼륨은 서로 다른 개념이다.
6. Windows 11은 TPM 2.0 등 보안 요구 사항이 있다.
7. 설치 후 UEFI, GPT, NTFS, TPM 등 시스템 구성을 검증해야 한다.
8. VMware 스냅샷으로 실습 환경의 상태를 보존할 수 있다.

**학습 상태: 1장 2교시 이론 및 실습 완료**
