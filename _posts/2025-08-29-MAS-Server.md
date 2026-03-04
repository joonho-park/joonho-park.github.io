---
layout: post
title:  "MAS-Server"
start_date: 2023-05-03
end_date: 2025-08-29
excerpt: "Monitoring Application System Server"
project: true
company: "Doople"
tags:
- project
comments: false
---

## MAS-Server

Postgre DB 쿼리, Redis Pub/Sub 등 을 이용한 서버 프로그램 개발.

Client, 장비서버 간 통신을 위한 중간다리 역할, 장비서버 와의 통신, Agent와의 Redis 통신 , Application 제어, HAProxy 상태 정보 확인 등 다양한 역할 수행

🎯 Core API 기능 (RESTful Endpoints)
1. Monitoring API
•	HAProxy 서버 상태 조회 (GetHaProxyStatus(GetProxyStatusModel[]))
•	프로세스 리소스 모니터링 (GetProcessResource(string))
•	Redis 키 초기화 (InitRedisKeys())
•	이상 이력 모니터링 조회 (GetAbnormalHistoryMonitoring(string, AbnormalyType, DateTime, DateTime))
•	Top5 이상 유형 통계 (GetTop5AbnormalType(DateTime, string))
•	서버 활성화/비활성화 제어 (EnableServer(string, string, string, bool))
•	전송 임계값 관리 (GetTransmissionThreshold(), InsertTransmissionThreshold(int, string, DateTime))
2. Configuration Management API
•	인스턴스 설정 조회/생성/수정/삭제
•	설정 배포 및 롤백 (DeployConfig, RollbackConfig)
•	설정 이력 관리 (GetConfigHistory)
•	도메인별 설정 관리 (GetConfigByDomain)
•	Live 설정 조회 (GetLiveConfig)
•	설정 새로고침 (RefreshConfig)
•	설정 패치 적용 (PatchConfig)
•	버전 관리 및 비교
3. Application Detail API
•	Consumer 상세 정보 조회
•	Consumer 실행 제어 (Start/Stop/Restart)
•	Consumer 백업/복원
•	Consumer 등록/삭제
•	Consumer 상태 모니터링
•	Consumer 그룹 관리
4. Equipment Detail API
•	장비 목록 조회
•	장비 상세 정보
•	장비 상태 모니터링
•	장비별 ACL 매핑 정보
•	장비 알람 설정
5. Data Transmission Status API
•	실시간 데이터 전송 상태 조회
•	추적 데이터 조회 (GetTrackingData)
•	이상 이력 조회 및 통계
•	세션 복구 이력 (GetSessionRecoveryHistory)
•	운영 로그 조회 (GetOperationLog)
•	전송 지연 분석
6. User Management API
•	사용자 계정 관리 (CRUD)
•	ACL 세션 관리
•	권한 관리
•	사용자 인증/인가
7. Consumer Registration API
•	Consumer 등록/해제
•	Consumer 그룹 관리
•	Consumer 설정 관리
---
⚙️ Background Services (7개)
1. AbnormalHistoryCollect
•	Redis Streams 기반 실시간 이상 이력 수집
•	배치 처리 (100건 단위)
•	DB 트랜잭션 보장
•	자동 알람 발송 (Missing, NotComing)
2. AbnormalHistorySummaryService
•	이상 이력 통계 집계
•	시간대별/유형별 요약
•	Top5 분석
3. SystemResourceCollect
•	시스템 리소스 모니터링 (CPU, Memory, Disk)
•	프로세스별 리소스 수집
•	Redis 저장
4. TransmissionStatusHistoryService
•	데이터 전송 이력 수집
•	지연 분석
•	통계 생성
5. EquipmentStatusAlarmService
•	장비 상태 감시
•	이상 상태 감지 시 알람
•	임계값 기반 알람
6. SessionRecoveryService
•	Consumer 세션 자동 감지
•	연결 끊김 시 자동 복구
•	복구 이력 기록
7. RedisSubscribeService
•	Redis Pub/Sub 이벤트 구독
•	실시간 메시지 처리
•	이벤트 라우팅
---
🔧 Core Infrastructure 기능
1. Redis 통합
•	Redis Streams 처리
•	Pub/Sub 메시징
•	Master-Slave 자동 감지
•	Connection Pooling
•	Key 관리
2. Database 처리
•	Multi-DB 지원 (Oracle, SQL Server)
•	배열 파라미터 기반 Bulk Insert
•	트랜잭션 관리
•	Connection Pooling
•	동적 쿼리 실행 (XML 기반)
3. HAProxy 통합
•	백엔드 서버 상태 조회
•	서버 활성화/비활성화
•	Health Check
•	통계 조회
4. Alarm System
•	HynixAlarm 연동
•	실시간 알람 발송
•	FAB/Area별 라우팅
•	알람 이력 관리
5. 메모리 최적화
•	ArrayPool 기반 객체 풀링
•	Zero-Allocation 파싱
•	IDisposable 패턴
•	GC 최적화
---
📊 데이터 처리 기능
1. 파싱 시스템
•	Redis Stream Entry 파싱
•	고성능 메모리 풀링
•	타입 안전 변환
•	에러 핸들링
2. 배치 처리
•	100건 단위 배치
•	트랜잭션 보장
•	실패 시 롤백
•	재시도 메커니즘
3. 실시간 추적
•	TraceId 기반 추적
•	데이터 흐름 모니터링
•	지연 측정
•	이상 감지
---
🛡️ 시스템 안정성 기능
1. HA (High Availability)
•	Master 노드 기반 작업 분산
•	자동 Failover
•	Health Check
•	상태 모니터링
2. 에러 처리
•	구조화된 로깅 (ILogger)
•	Exception 추적
•	자동 복구
•	알림 시스템
3. 성능 모니터링
•	Stopwatch 기반 성능 측정
•	처리 시간 추적
•	리소스 사용량 모니터링
•	병목 지점 식별
---
🔐 보안 기능
•	암호화 (Encryption 라이브러리)
•	사용자 인증/인가
•	ACL 기반 권한 관리
•	세션 관리
---
📈 분석 및 리포팅
•	이상 통계 생성
•	Top5 분석
•	시간대별 집계
•	대시보드 데이터 제공
•	운영 로그 분석
---
🔄 통합 기능
•	HAS Client API 연동
•	Agent Client API 연동
•	OpenAPI 스펙 지원
•	NSwag 기반 클라이언트 생성
---
총 7개 BackgroundService + 50+ API Endpoints + 다중 Repository + 통합 Infrastructure

지표	       |성과
실시간 처리량	|500+ 건/초
응답 속도 개선  |3배 향상 (150ms → 50ms)
GC 부하 감소	|90% 감소
데이터 유실률	|0%
시스템 Uptime  |99.9%
자동 복구율	    |98%
운영 효율 향상	|40%
다운타임 감소	|30%


[[PPT] MAS-Server](/assets/pdf/MAS-Server.pdf)