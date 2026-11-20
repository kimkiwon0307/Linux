<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/646a5f08-ba1e-4221-a5c8-14a6edf6e746" />


# Windows OS 프로젝트식 학습
## 2장 1교시 — Windows 시스템 관리

### 1. 핵심 개념

| 개념 | 설명 |
|---|---|
| Process | 실행 중인 프로그램 |
| Service | Windows가 시작·중지·상태를 관리하는 서비스 프로그램 |
| Event Log | 시스템과 프로그램에서 발생한 이벤트 기록 |
| Task Scheduler | 정해진 시간이나 조건에 작업을 자동 실행하는 기능 |
| Performance Monitor | CPU·메모리·디스크 등 시스템 성능 확인 |

### 2. CMD와 PowerShell 차이

- **CMD:** Windows의 기본적인 명령어 실행 환경
- **PowerShell:** 객체 기반 시스템 관리 및 자동화 도구

PowerShell은 여러 서버를 일괄 점검하거나 반복 작업을 자동화할 때 유용하다.

### 3. Windows GUI 관리 도구

| 도구 | 실행 명령어 | 역할 |
|---|---|---|
| 작업 관리자 | `taskmgr` | 프로세스·CPU·메모리 확인 |
| 서비스 관리 | `services.msc` | 서비스 상태·시작 유형 관리 |
| 이벤트 뷰어 | `eventvwr.msc` | 시스템·응용 프로그램 로그 확인 |
| 성능 모니터 | `perfmon` | 시스템 성능 분석 |
| 리소스 모니터 | `resmon` | 자원 사용량 상세 확인 |
| 작업 스케줄러 | `taskschd.msc` | 반복 작업 자동 실행 |

### 4. PowerShell 핵심 명령어

```powershell
# 프로세스 확인
Get-Process

# 서비스 상태 확인
Get-Service

# 특정 서비스 확인
Get-Service -Name EventLog

# 최근 시스템 이벤트 10개 조회
Get-WinEvent -LogName System -MaxEvents 10
```

**필수 암기 명령어**
- `Get-Process`: 프로세스 확인
- `Get-Service`: 서비스 확인
- `Get-WinEvent`: 이벤트 로그 확인

### 5. 작업 스케줄러 동작 원리

- **Trigger:** 언제 실행할 것인가?
- **Action:** 무엇을 실행할 것인가?

예시: 매일 오전 9시에 시스템 점검 스크립트 자동 실행

### 6. Windows와 Linux 비교

| Windows | Linux | 목적 |
|---|---|---|
| Get-Process | ps aux | 프로세스 확인 |
| Get-Service | systemctl | 서비스 관리 |
| Get-WinEvent | journalctl | 로그 확인 |
| 작업 관리자 | top, htop | 자원 확인 |
| 작업 스케줄러 | cron | 작업 자동화 |

### 7. 실무 장애 대응

**상황: Windows 서버에서 프로그램이 응답하지 않는 경우**

1. `Get-Process` → 프로세스 실행 여부 확인
2. `Get-Service` → 관련 서비스 상태 확인
3. `Get-WinEvent` → 오류 로그 확인
4. 작업 관리자·성능 모니터 → CPU·메모리 등 자원 확인
5. 원인 분석 후 조치 및 정상 동작 재검증

※ 서비스가 Running 상태여도 프로그램이 정상 작동한다는 보장은 없다.

### 8. 최종 핵심 암기

1. **Process:** 실행 중인 프로그램
2. **Service:** Windows가 관리하는 서비스 프로그램
3. **Event Log:** 장애 분석을 위한 이벤트 기록
4. **Task Scheduler:** 반복 작업 자동화
5. **PowerShell:** Windows 시스템 관리 및 자동화
6. **장애 대응:** 상태 확인 → 로그 확인 → 원인 분석 → 조치 → 재검증

**학습 상태: 2장 1교시 완료**
