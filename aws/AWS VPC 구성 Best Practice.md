# AWS VPC 구성 Best Practice

AWS VPC 구성에 대한 Best Practice는 고가용성, 보안, 확장성, 그리고 네트워크 관리의 효율성을 고려한 네트워크 아키텍쳐를 구축하는 데 중점을 둡니다. 이를 바탕으로 한 VPC 구성 방식은 다음과 같습니다.

1. VPC 설계

- VPC는 AWS 내에서 사용자가 네트워크를 정의할 수 있는 가상 네트워크입니다. VPC의 CIDR 블록을 통해 IP 주소 범위를 지정합니다. 보통 `/16` 블록을 사용하여 최대 65,536개의 IP 주소를 사용할 수 있습니다. 예를 들어 `10.0.0.0/16`과 같은 IP 범위를 사용할 수 있습니다.

2. 서브넷 구성

퍼블릭 서브넷과 프라이빗 서브넷(어플리케이션 서브넷), 그리고 데이터베이스 서브넷으로 나누어 리소스를 배치합니다.

- 퍼블릭 서브넷: 외부 인터넷과 연결되는 서브넷으로, 주로 웹 서버나 로드밸런서가 배치됩니다.
- 프라이빗 서브넷(어플리케이션 서브넷): 인터넷에 직접 연결되지 않는 서브넷으로, 어플리케이션 서버나 백엔드 서비스가 배치됩니다.
- 데이터베이스 서브넷: 민감한 데이터를 보관하는 데이터베이스 서버가 배치되며, 외부로의 직접 연결은 허용되지 않습니다.

3. 가용 영역(AZ) 활용

AWS 리전 내 여러 가용 영역(AZ)에 서브넷을 분산 배치하여 고아용성을 확보합니다. 예를 들어, 세 개의 가용 영역을 사용할 때, 각 가용 영역에 퍼블릭 서브넷, 애플리케이션 서브넷, 데이터베이스 서브넷을 배치합니다. 이를 통해 장애가 발생해도 다른 AZ에서 서비스가 지속될 수 있습니다.

4. 라우팅 테이블 구성

라우팅 테이블은 각 서브넷의 트래픽이 어디로 이동할지 결정합니다.

- 퍼블릭 서브넷의 라우팅 테이블: 인터넷 게이트웨이(IGW)를 통해 외부 인터넷과 연결됩니다. `0.0.0.0/0` 경로는 모든 외부 트래픽을 인터넷 게이트웨이로 라우팅합니다.
  - 예: `0.0.0.0/0 -> Internet Gateway`
- 프라이빗 서브넷(어플리케이션 서브넷)의 라우팅 테이블: 외부로 나가는 트래픽은 NAT 게이트웨이를 통해 라우팅됩니다. 프라이빗 서브넷에서 직접 인터넷에 접근하지 않고 NAT 게이트웨이를 경유합니다.
  - 예: `0.0.0.0/0 -> NAT Gateway`
- 데이터베이스 서브넷의 라우팅 테이블: 외부로 나가는 트래픽을 전혀 허용하지 않으며, 오직 VPC 내의 어플리케이션 서브넷에서만 접근이 가능합니다. 인터넷으로의 트래픽 경로는 설정하지 않습니다.
  - 예: `NO 0.0.0.0/0 entry`

5. 인터넷 게이트웨이(IGW)와 NAT 게이트웨이

- 인터넷 게이트웨이(IGW)는 퍼블릭 서브넷에서 외부 인터넷과 연결할 수 있도록 하며, 퍼블릭 서브넷에 배치된 모든 리소스는 이 게이트웨이를 통해 외부와 통신합니다.
- NAT 게이트웨이는 프라이빗 서브넷에서 외부로 나가는 트래픽을 처리합니다. 프라이빗 서브넷의 인스턴스가 외부 인터넷으로 나갈 떄는 NAT 게이트웨이를 통해서만 가능합니다.

6. 보안 그룹과 네트워크 ACL

- 보안 그룹(Security Group): 각 인스턴스에 대한 방화벽 역할을 하며, 인바운드 트래픽을 제어합니다. 보안 그룹은 상태 저장 방식(stateful)으로 동작하며, 인바운드 트래픽을 허용하면 그에 따른 아웃바운드 트래픽도 자동으로 허용됩니다.
- 네트워크 ACL(NACL): 서브넷 단위에서 트래픽을 제어하는 방식으로 상태 비저장(stateless) 방식으로 동작합니다. NACL은 인바운드와 아웃바운드 트래픽을 명시적으로 설정해야 하며, 여러 서브넷에 적용할 수 있습니다.

7. VPC 엔드포이트

VPC 엔드포인트는 인터넷을 거치지 않고 AWS 서비스와 안전하게 통신할 수 있도록 합니다.

- 인터페이스 엔드포인트: S3, DynamoDB 이외의 다른 AWS 서브시에 안전하게 접근할 수 있도록 해줍니다.
- 게이트웨이 엔드포인트: S3, DynamoDB에 대한 전용 통신 경로를 제공합니다.

8. 고가용성 설계

고가용성을 유지하기 위해 각 가용 영역에 서브넷을 나누어 배포하고, 로드 밸런서를 사용해 트래픽을 여러 가용 영역에 분산시킵니다. 또한 각 가용 영역마다 NAT게이트웨이를 배치하여, 한 AZ에서 장애가 발생해도 다른 AZ에서 NAT 게이트웨이를 통해 외부로의 트래픽치 처리될 수 있습니다.

9. 모니터링 및 로깅

- VPC 흐름 로그 (VPC Flow Logs): VPC에서 주고받는 트래픽을 로그로 기록하여 네트워크 트래픽을 모니터링하고 분석할 수 있습니다.
- Amazon CloudWatch: 네트워크와 리소스 상태를 실시간으로 모니터링하고 경고를 설정할 수 있습니다.
- AWS CloudTrail: VPC 관련 설정 변경과 같은 이벤트를 기록하여 추적할 수 있습니다.

10. 멀티 VPC 연결

- VPC 피어링: 동일 리전 또는 다른 리전에 있는 VPC 간에 직접적인 네트워크 통신을 가능하게 합니다. AWS 네트워크 내에서 트래픽을 전달하므로 보안성과 성능이 뛰어납니다.
- AWS Transit Gateway: 여러 VPC와 온프레미스 네트워크를 연결하고 관리할 수 있는 중앙 허브 역할을 합니다.

1. VPC 및 Direct Connect

- AWS Site-to-Site VPN: 온프레미스 네트워크와 AWS 간의 안전한 가상사설 네트워크를 설정할 수 있습니다.
- AWS Direct Connect: 고대역폭 전용 네트워크 링크를 사용하여 온프레미스 데이터센터와 AWS를 연결할 수 있습니다.
