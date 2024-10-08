# Jenkins 아키텍처

Jenkins는 **플러그인 기반**의 오픈 소스 **자동화 서버**로, 주로 CI/CD 파이프라인을 관리하는 데 사용됩니다. Jenkins의 아키텍처는 매우 유연하며 확장성이 뛰어난 구조로, 다양한 환경과 요구 사항을 처리할 수 있습니다. Jenkins 아키텍처는 크게 **마스터-에이전트(Master-Agent)** 구조로 나뉩니다.

## 1. **Jenkins 마스터 (Jenkins Master)**

Jenkins 마스터는 CI/CD 파이프라인의 중심 역할을 수행하며, Jenkins의 주요 기능을 관리합니다.

### 주요 기능

- **사용자 인터페이스 제공**: Jenkins 웹 UI를 통해 사용자들이 파이프라인을 구성하고 관리할 수 있습니다.
- **잡(빌드) 관리**: 빌드 스케줄을 관리하고, 실행할 빌드 작업을 큐에 넣습니다.
- **에이전트 할당**: 특정 빌드 작업을 어느 에이전트에서 실행할지 결정하고 할당합니다.
- **결과 수집 및 리포팅**: 빌드 및 테스트 결과를 수집하고 사용자에게 알림 및 보고서를 제공합니다.
- **플러그인 관리**: Jenkins의 기능을 확장하는 다양한 플러그인을 관리하고, 플러그인 간의 통합을 처리합니다.

Jenkins 마스터는 빌드 작업을 관리하고 배포 환경을 조정하는 핵심적인 부분으로, 모든 주요 작업의 흐름을 담당합니다.

## 2. **Jenkins 에이전트 (Jenkins Agent)**

Jenkins 에이전트는 마스터로부터 할당받은 빌드 작업을 실제로 수행하는 역할을 합니다. 여러 에이전트가 Jenkins 마스터에 연결되어 병렬로 작업을 처리할 수 있습니다.

### 주요 역할

- **빌드 실행**: 마스터에서 요청한 빌드 작업을 실행하고 그 결과를 마스터에게 전달합니다.
- **테스트 실행**: 테스트를 실행하고 결과를 마스터에 보고합니다.
- **다양한 환경에서 실행 가능**: 에이전트는 다양한 운영 체제 및 환경에서 실행될 수 있습니다(예: Windows, Linux, Docker 컨테이너 등).

에이전트를 사용하면 Jenkins 마스터의 부하를 줄이고, 다양한 환경에서 빌드 및 테스트를 분산 처리할 수 있습니다.

## 3. **마스터-에이전트 통신**

Jenkins 마스터와 에이전트는 서로 **통신**하여 빌드 작업을 수행하고 결과를 주고받습니다. 이 통신은 여러 가지 방법을 통해 설정할 수 있으며, 다음과 같은 프로토콜과 메커니즘이 있습니다:

- **SSH**: 가장 일반적으로 사용되는 통신 방식으로, 에이전트가 SSH를 통해 마스터와 연결됩니다.
- **JNLP**: Java Network Launch Protocol을 사용하여 마스터와 에이전트가 통신합니다.
- **WebSocket**: 현대적 환경에서는 WebSocket을 통한 통신도 지원됩니다.

## 4. **플러그인 시스템**

Jenkins의 강력한 점 중 하나는 **플러그인 시스템**입니다. Jenkins는 수천 개의 플러그인을 제공하여 CI/CD 파이프라인의 거의 모든 요구 사항을 처리할 수 있습니다. 주요 플러그인 역할은 다음과 같습니다:

- **빌드 도구 통합**: Maven, Gradle, Node.js와 같은 빌드 도구를 통합.
- **소스 코드 관리**: Git, SVN 등과 통합하여 소스 코드를 관리하고 변경 사항을 감지.
- **테스트 및 코드 품질 도구**: JUnit, Selenium, SonarQube 등과 통합하여 테스트 및 코드 품질 검사.
- **알림 및 배포 도구**: Slack, 이메일, Kubernetes, Docker와 통합하여 알림 및 자동 배포.

플러그인은 Jenkins의 기능을 확장하고, 사용자 요구에 맞게 파이프라인을 커스터마이징할 수 있는 중요한 요소입니다.

## 5. **파이프라인 (Pipeline)**

Jenkins 파이프라인은 코드로서 CI/CD 프로세스를 정의할 수 있는 기능을 제공합니다. Jenkins는 기본적으로 **선언형 파이프라인**과 **스크립트형 파이프라인** 두 가지 방식을 지원합니다.

- **선언형 파이프라인**: 간단한 문법으로 파이프라인을 정의하는 방식. YAML과 비슷한 구문을 사용하여 파이프라인을 설정.
- **스크립트형 파이프라인**: 더 복잡한 논리와 조건을 사용할 수 있는 Groovy 기반의 스크립트 언어로 정의.

파이프라인을 통해 빌드, 테스트, 배포의 전체 과정을 자동화할 수 있으며, 이를 **Jenkinsfile**에 정의하여 코드로 관리할 수 있습니다.

## 6. **Jenkins 분산 빌드**

Jenkins는 에이전트를 사용하여 **분산 빌드**를 지원합니다. 마스터는 빌드 스케줄링과 관리만 수행하고, 실제 빌드와 테스트는 에이전트에서 병렬로 실행됩니다. 이를 통해 다음과 같은 이점이 있습니다:

- **병렬 빌드**: 여러 에이전트에서 동시에 빌드를 실행하여 빌드 속도를 높일 수 있습니다.
- **다양한 환경에서 테스트**: 다양한 운영 체제와 환경에서 빌드 및 테스트를 수행할 수 있습니다.
- **확장성**: 에이전트를 추가하여 빌드 및 테스트 용량을 확장할 수 있습니다.

## 7. **Jenkins 아키텍처 요약**

- **마스터-에이전트 구조**: 마스터는 빌드 관리, 에이전트는 실제 빌드 실행.
- **플러그인 기반 확장성**: 플러그인을 통해 다양한 도구 및 플랫폼과 통합.
- **파이프라인**: CI/CD 프로세스를 코드로 정의하고 자동화.
- **분산 빌드**: 에이전트를 활용한 병렬 빌드 및 다양한 환경에서 테스트 수행.

Jenkins는 유연하고 확장성이 뛰어난 아키텍처 덕분에 대규모 프로젝트에서도 안정적으로 사용할 수 있는 CI/CD 도구로 자리 잡고 있습니다.
