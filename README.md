# Cisco-Enterprise-Network
# Cisco 기반 Enterprise Network 설계·구축·장애 대응 및 네트워크 자동화 LAB

Cisco 기반의 Enterprise Network 환경을 직접 설계하고 구축하며,  
네트워크 장애 상황을 의도적으로 재현하고 원인을 분석·복구하는 실습 프로젝트입니다.

단순한 Cisco 명령어 실습을 넘어 **기업 네트워크의 설계 → 구축 → 검증 → 장애 대응 → 자동화**까지 경험하는 것을 목표로 합니다.

---

## 1. Project Overview

### 프로젝트 목적

- Enterprise Network 구조 및 설계 방법 이해
- Cisco Router / Switch 기반 네트워크 구축
- VLAN 및 Inter-VLAN Routing 구성
- OSPF 기반 동적 라우팅 구성
- 네트워크 이중화 및 고가용성 구성
- ACL을 이용한 네트워크 접근 제어
- NAT/PAT을 이용한 외부 네트워크 연결
- 실제 장애 상황을 가정한 트러블슈팅
- 반복적인 네트워크 운영 작업 자동화

### Project Environment

| Category | Environment |
|---|---|
| Network Simulator | Cisco Packet Tracer |
| Vendor | Cisco |
| Routing | Static Routing / OSPF |
| Switching | VLAN / Trunk / STP / EtherChannel |
| Redundancy | HSRP |
| Security | ACL / SSH / VLAN Segmentation |
| Internet Access | NAT / PAT |
| Automation | Python / Ansible |
| Documentation | GitHub |

---

## 2. Network Architecture

본 프로젝트에서는 중견기업의 본사 네트워크를 가정하여 설계합니다.

```text
                         INTERNET
                            │
                       [ EDGE-R1 ]
                            │
                       [ FIREWALL ]
                            │
                ┌───────────┴───────────┐
                │                       │
            [ CORE-SW1 ]═══════════[ CORE-SW2 ]
                │                       │
        ┌───────┼───────┐       ┌───────┼───────┐
        │       │       │       │       │       │
      [SW1]   [SW2]   [SW3]   SERVER    AP    Management
        │       │       │
       PC      PC      PC
```

### Network Segmentation

| VLAN | Name | Network | Purpose |
|---:|---|---|---|
| 10 | HR | 10.10.10.0/24 | 인사팀 |
| 20 | DEV | 10.10.20.0/24 | 개발팀 |
| 30 | SALES | 10.10.30.0/24 | 영업팀 |
| 40 | SERVER | 10.10.40.0/24 | 서버 |
| 50 | MGMT | 10.10.50.0/24 | 네트워크 관리 |
| 60 | GUEST | 10.10.60.0/24 | Guest Network |

---

## 3. Network Design

### Core Layer

- CORE-SW1
- CORE-SW2
- Inter-VLAN Routing
- OSPF
- HSRP
- 네트워크 핵심 구간 이중화

### Access Layer

- SW1
- SW2
- SW3
- VLAN
- Access Port
- Trunk
- STP
- EtherChannel

### Edge Layer

- EDGE-R1
- Default Route
- NAT/PAT
- 외부 네트워크 연결

---

## 4. Implementation Roadmap

### Phase 1. Network Design

- [ ] 기업 환경 정의
- [ ] 네트워크 요구사항 분석
- [ ] 네트워크 토폴로지 설계
- [ ] VLAN 설계
- [ ] IP Addressing 계획
- [ ] 장비 역할 정의

### Phase 2. Basic Switching

- [ ] VLAN 구성
- [ ] Access Port 구성
- [ ] Trunk 구성
- [ ] STP 구성
- [ ] EtherChannel 구성
- [ ] 기본 통신 테스트

### Phase 3. Routing

- [ ] Inter-VLAN Routing
- [ ] Static Routing
- [ ] OSPF
- [ ] Default Route
- [ ] Routing Table 검증

### Phase 4. High Availability

- [ ] HSRP
- [ ] 링크 이중화
- [ ] 장비 이중화
- [ ] 장애 발생 시 Failover 테스트

### Phase 5. Network Security

- [ ] SSH 원격 관리
- [ ] Standard ACL
- [ ] Extended ACL
- [ ] VLAN 간 접근제어
- [ ] Guest Network 격리
- [ ] Management Network 보호

### Phase 6. Internet Connectivity

- [ ] Edge Router 구성
- [ ] NAT
- [ ] PAT
- [ ] Default Gateway
- [ ] 내부 ↔ 외부 통신 테스트

### Phase 7. Troubleshooting LAB

의도적으로 장애를 발생시키고 다음 절차에 따라 분석합니다.

```text
장애 발생
   ↓
증상 확인
   ↓
문제 구간 추정
   ↓
show 명령어를 통한 상태 확인
   ↓
원인 분석
   ↓
설정 수정
   ↓
통신 테스트
   ↓
정상 상태 확인
   ↓
장애 대응 문서화
```

### Phase 8. Network Automation

- [ ] Python 기반 장비 상태 확인
- [ ] Config Backup
- [ ] Interface 상태 수집
- [ ] Ping 자동 점검
- [ ] 장애 탐지
- [ ] Ansible 기반 Cisco 장비 관리

---

## 5. Troubleshooting Scenarios

프로젝트 진행 과정에서 다음과 같은 장애 상황을 직접 재현합니다.

| Scenario | 주요 확인 내용 |
|---|---|
| VLAN 통신 장애 | VLAN / Access Port |
| Trunk 장애 | Trunk / Allowed VLAN |
| Inter-VLAN 통신 장애 | SVI / Gateway |
| OSPF Neighbor 장애 | OSPF 설정 / Interface |
| Routing 장애 | Routing Table |
| ACL 통신 차단 | ACL Rule |
| STP 문제 | Root Bridge / Port State |
| EtherChannel 장애 | Port-Channel 설정 |
| Interface 장애 | Interface Status |
| Gateway 장애 | HSRP |
| NAT 장애 | NAT Translation |
| SSH 접속 장애 | SSH / VTY / Authentication |

---

## 6. Troubleshooting Documentation

각 장애는 다음과 같은 형식으로 기록합니다.

### Example

**Problem**

> DEV VLAN에서 SERVER VLAN으로 통신이 불가능한 현상 발생

**Symptoms**

```text
PC → Gateway       정상
PC → 다른 VLAN     실패
PC → Server        실패
```

**Investigation**

```text
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
show access-lists
```

**Root Cause**

> ACL 설정 오류로 인해 DEV VLAN에서 SERVER VLAN으로 향하는 트래픽이 차단됨

**Resolution**

> ACL 정책 수정 후 정상 통신 확인

**Verification**

```text
ping 10.10.40.x
```

**Result**

> 정상 통신 확인

---

## 7. Project Goals

이 프로젝트를 통해 다음과 같은 역량을 확보하는 것을 목표로 합니다.

- Enterprise Network 설계 능력
- Cisco 장비 구축 및 설정 능력
- Routing / Switching 이해
- Network Security 구성 능력
- 장애 원인 분석 및 Troubleshooting 능력
- 네트워크 이중화 구성 경험
- 네트워크 운영 자동화 경험
- 네트워크 구성 및 장애 대응 문서화

---

## 8. Project Status

> 🚧 현재 프로젝트 구축 진행 중

### Current Progress

- [x] 프로젝트 방향 설정
- [x] Enterprise Network 구조 설계
- [x] VLAN / IP Addressing 초안
- [ ] Cisco Packet Tracer 환경 구축
- [ ] 장비 배치
- [ ] 기본 Switching 구성
- [ ] Routing 구성
- [ ] Network Security
- [ ] High Availability
- [ ] Troubleshooting LAB
- [ ] Network Automation
- [ ] 최종 문서화

---

## 9. Repository Structure

프로젝트가 진행되면서 다음과 같이 구성할 예정입니다.

```text
Cisco-Enterprise-Network/
│
├── README.md
│
├── 01_Network_Design/
│   ├── topology/
│   ├── ip_plan/
│   └── vlan_plan/
│
├── 02_Switching/
│   ├── vlan/
│   ├── trunk/
│   ├── stp/
│   └── etherchannel/
│
├── 03_Routing/
│   ├── static/
│   ├── ospf/
│   └── inter_vlan/
│
├── 04_High_Availability/
│   └── hsrp/
│
├── 05_Security/
│   ├── acl/
│   └── ssh/
│
├── 06_NAT/
│   └── nat_pat/
│
├── 07_Troubleshooting/
│   ├── vlan_issue/
│   ├── routing_issue/
│   ├── ospf_issue/
│   ├── acl_issue/
│   └── stp_issue/
│
├── 08_Automation/
│   ├── python/
│   └── ansible/
│
└── packet_tracer/
    └── enterprise_network.pkt
```

---

## 10. Final Objective

최종적으로 다음과 같은 흐름을 갖는 Enterprise Network LAB을 완성합니다.

```text
             설계
              ↓
             구축
              ↓
             검증
              ↓
          장애 상황 재현
              ↓
          원인 분석
              ↓
             복구
              ↓
            자동화
              ↓
           문서화
```

단순한 네트워크 설정 실습이 아닌, **기업 네트워크를 직접 설계하고 구축한 뒤 장애 대응과 운영 자동화까지 수행하는 프로젝트**를 목표로 합니다.
