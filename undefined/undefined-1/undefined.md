# 검증자 실행하기

이 섹션에서는 [Mainnet](mainnet.md)에서 검증자 노드를 실행하는 방법에 대해 설명합니다. 

{% hint style="info" %}
검증, 노드 운영 및 거버넌스를 포함하여 셀로 커뮤니티에서 일어나는 모든 뉴스를 최신 상태로 유지하려면 [Celo Signal 메일링 목록](https://celo.activehosted.com/f/15)에 등록하세요!

관련 날짜들이 등록되어 있는  [Celo Signal 공용 캘린더](https://calendar.google.com/calendar/u/0/embed?src=c_9su6ich1uhmetr4ob3sij6kaqs@group.calendar.google.com)도 추가할 수 있습니다.
{% endhint %}

검증자는 Celo의 지분 증명 프로토콜에 참여함으로써 Celo 네트워크를 보호하는 데 도움을 줍니다. 검증자들은 대의민주주의 정당과 유사한 검증자 그룹으로 구성됩니다. 검증자 그룹은 기본적으로 검증자들의 정렬된 목록입니다.

민주주의에 속한 모든 사람이 자신의 정당을 만들 수 있고 정당을 대표하기 위해 선거에서 표를 받으려고 하는 것처럼, Celo 사용자는 누구나 검증자 그룹을 만들어 거기에 자신을 더하거나, 잠재적인 검증자를 설정하고 기존 검증자 그룹을 영입하기 위해 일할 수 있습니다.

Celo 네트워크에는 다른 검증자 그룹들이 존재하지만, 검증자 그룹을 등록하여 실행하는 가장 빠른 방법은 검증자 그룹을 등록하고 검증자를 검증자 그룹에 가입시키는 것입니다. 검증자 그룹 및 검증자를 등록하는 데 사용되는 주소는 고유해야 합니다. 그래서 아래 단계별 가이드를 따라 두 개의 계정을 만들어야 합니다.

검증자 보안 및 가용성의 중요성 때문에 검증자는 각 검증자 노드 앞에서 "프록시" 노드를 실행해야 합니다. 이 설정에서 프록시 노드는 네트워크의 나머지 부분들과 연결되고 검증자 노드는 개인 네트워크를 통해 프록시와만 통신합니다.

또한 검증자는 사용자가 휴대폰 번호를 셀로 주소에 매핑할 수 있도록 허용하는 증명을 제공하기 위해 [lightweight identity protocol](../celo-codebase/protocol/identity)의 일부로 [Attestation Service](https://github.com/celo-org/celo-monorepo/tree/master/packages/attestation-service)를 실행해야 합니다.

[Celo의 미션과 검증자가 되면 좋은 이유에 대해 좀 더 자세히 읽어보세요.](https://medium.com/celoorg/calling-all-chefs-become-a-celo-validator-c75d1c2909aa)

그리고 이 페이지에서는 검증을 위한 ReleaseGold 및 non-ReleaseGold 단계에 대한 별도의 단계도 제공합니다.

{% hint style="info" %}
Celo 검증자가 처음이시라면, Non-ReleaseGold 설명을 따라하세요.
{% endhint %}

## 필요 조건

### Staking 요구조건

셀로는 [지분 증명](../celo-codebase/protocol/proof-of-stake) 합의 메커니즘을 사용하므로 검증자가 블록 생산에 참여하기 위해서는 CELO를 보유하고 있어야 합니다. 현재는 검증자를 등록하는 데 10,000 CELO, 검증자 그룹을 등록하는 데에는 멤버당 10,000 CELO 가 요구됩니다.

필요한 CELO가 없는 경우 [Baklava에서 검증자 실행](running-a-validator-in-baklava.md)에 따라 Baklava 네트워크에서 검증자를 생성하는 프로세스를 시도할 수 있습니다.

여기서는 CELO 보유 유무에 대해 논의하지 않겠지만 필요한 CELO를 보유하고 있다는 것이 전제 조건이며, 이 가이드에서 사용자의 자금은 검증자와 검증자 그룹에 대한 두 가지 `ReleaseGold` 계약으로 보관된다고 가정합니다. 만약 그렇지 않은 경우 여기서 제공된 명령어를 조정해야 하지만 가이드는 여전히 필요한 단계를 제공할 것 입니다.

높은 수준에서 `ReleaseGold`는 계획된 출시 균형을 유지하고 있고, 컨트랙트 구성에 따라 유효성 확인 및 투표와 같은 특정 행동에는 보유하고 있는 잔액을 사용할 수 있도록 허용합니다. [`ReleaseGold`에 대해 더 알아보세요.](../celo-holder-guide/release-gold.md)

**Non-ReleaseGold**

{% hint style="info" %}
Celo 검증자가 처음이시라면, Non-ReleaseGold 설명을 따라하세요.
{% endhint %}

### **하드웨어 요구조건**

권장되는 Celo 검증자 설정에는 다음 세 가지 인스턴스를 지속적으로 실행하는 것을 포함하고 있습니다 :

* 1 **검증자 노드** : 고가용성\(HA\) 데이터 센터의 단일 테넌트 하드웨어에 구축해야 합니다.
* 1 **검증자 프록시 노드** : 멀티 테넌트\(예: 퍼블릭 클라우드\) 환경에서 VM 또는 컨테이너가 될 수 있지만 고가용성이 필요합니다.
* 1 **인증 노드** : 멀티 테넌트 환경\(예: 퍼블릭 클라우드\)에서 VM 또는 컨테이너가 될 수 있으며, 가용성 요구사항이 보통입니다.

Celo는 작업 증명 네트워크와는 다른 하드웨어 요구 사항을 가진 지분 증명 네트워크입니다. 지분 증명 합의는 CPU 집약도는 낮지만 네트워크 연결 및 지연 시간에 더 민감합니다. 다음은 Celo 네트워크에서 검증자 및 프록시 노드를 실행하기 위한 표준 요구 사항 목록입니다.

* 메모리 : 8GB RAM
* CPU : 쿼드 코어 3GHz\(64비트\)
* 디스크 : 256GB의 SSD 스토리지와 보조 HDD가 바람직함
* 네트워크 : 최소 1GB의 입/출력 이더넷\(섬유 인터넷 연결, 이상적인 중복 연결 및 HA 스위치 포함\)

증명 서비스 노드는 리소스를 적게 사용하고 메모리 및 컴퓨팅이 적은 시스템에서 실행될 수 있습니다.

또한 작업을 시작하려면 CLI 명령을 실행할 수 있는 노드를 로컬 시스템에서 실행하는 것이 유용합니다.

### 네트워킹 요구조건

검증자가 합의되고 완전한 증명에 참여하려면 네트워크를 올바르게 구성하는 것이 매우 중요합니다.

프록시 및 증명 노드에는 정적 외부 IP 주소가 있어야 하며 검증자 노드가 내부 네트워크 또는 프록시의 외부 IP 주소를 통해 프록시와 통신할 수 있어야 합니다.

검증자 시스템에서 포트 30503은 프록시 시스템의 IP 주소에서 TCP 연결을 수락해야 합니다. 이 포트는 검증자가 프록시와 통신하는 데 사용됩니다.

프록시 시스템에서 포트 30503은 검증자 시스템의 IP 주소에서 TCP 연결을 수락해야 합니다. 이 포트는 프록시가 검증자와 통신하는 데 사용됩니다.

프록시 및 증명 시스템에서 포트 30303은 모든 IP 주소에서 TCP 및 UDP 연결을 허용해야 합니다. 이 포트는 네트워크의 다른 노드와 통신하는 데 사용됩니다.

증명 시스템에서 포트 80은 모든 IP 주소의 TCP 연결을 승인해야 합니다. 이 포트는 사용자가 사용자로부터 증명을 요청하는 데 사용됩니다.

다음 표를 참조하세요 :

| 장비 \ IP 수락 | 0.0.0.0/0 \(all\) | 검증자 ip | 프록시 ip |
| :--- | :--- | :--- | :--- |
| 검증자 |   |   | tcp:30503 |
| 프록시 | tcp:30303, udp:30303 | tcp:30503 |   |
| 인증 | tcp:80 |   |   |

### 소프트웨어 요구조건

#### 각 기계에서 필요한 조건

* **Docker가 설치되어 있어야 합니다.** 만약 Docker가 설치되어 있지 않은 경우, 다음 절차를 따르세요 : [Docker 시작하기](https://www.docker.com/get-started). Docker 계정을 생성하거나 로그인하고 데스크톱 앱을 다운로드한 후 Docker CLI를 사용할 수 있도록 앱을 시작할 수 있도록 하는 설명이 포함되어 있습니다.  리눅스 서버에서 실행 중인 경우 [distro](https://docs.docker.com/install/#server)의 설명을 따라하세요. 설치 환경에 따라 `sudo`로 Docker를 실행해야 할 수도 있습니다. `docker info` 가 제대로 작동한다면 Docker가 제대로 설치되어 실행 중이라는 뜻입니다.

#### 로컬 컴퓨터에서 필요한 조건

* **Celocli가 설치되어 있어야 합니다.** [Command Line Interface \(CLI\)](../command-line-interface/introduction.md) 을 참고해서 설정하세요. 
* **최신 Node.js v12.x를 사용하고 있어야 합니다.** 일부 사용자는 최신 버전의 노드를 사용하여 문제를 보고했습니다. 신뢰도를 높이려면 LTS를 사용하십시오.

{% hint style="info" %}
규칙에 대한 참고 사항 : 이 페이지에 표시되는 코드 조각들은 bash 명령어와 그에 따른 출력입니다. 

&lt;&gt;의 각괄호 안에 텍스트가 있으면 해당 텍스트를 그 안의 텍스트를 참조하는 고유한 값으로 바꿔주세요. bash 명령에 &lt;&gt;를 포함하지 마세요.
{% endhint %}

### 키 관리

개인 키는 모든 암호화 시스템의 중심이 되는 키이므로 매우 주의하여 처리해야 합니다. 개인 키를 잃어버리면 되돌릴 수 없는 가치 손실이 발생할 수 있습니다.

이 가이드에는 많은 수의 키가 포함되어 있으므로 각 키의 목적을 이해하는 것이 중요합니다.   
[키 관리에 대해 더 알아보세요.](../validator-guide/key-management/summary.md)

#### 잠금 해제

셀로 노드는 암호로 암호화된 개인 키를 디스크에 저장하므로 사용하기 전에 "잠금 해제"해야 합니다. 개인 키는 두 가지 방법으로 잠금 해제할 수 있습니다. :  
  
1. `celocli account:unlock` 명령을 실행합니다. 이 명령이 작동되려면 노드가 "개인" RPC API를 사용하도록 설정되어 있어야 합니다.  
2. 노드를 시작할 때 `--unlock` 플래그를 실행합니다.

키가 잠금 해제된 경우 노드의 RPC API에 대한 액세스를 활성화하는 것을 특히 주의해야 합니다. 

### 환경변수

이 가이드에는 여러 환경 변수가 있으며, 이 표를 참고하세요.

| 변수 | 설명 |
| :--- | :--- |
| CELO\_IMAGE | 검증자 및 프록시 컨테이너에 사용되는 도커 이미지 |
| CELO\_VALIDATOR\_GROUP\_ADDRESS | 검증자 그룹의 계정 주소 \(= 검증자 그룹의 `ReleaseGold` 수령 주소\) |
| CELO\_VALIDATOR\_ADDRESS | 검증자의 계정 주소 \(= 검증자의 `ReleaseGold` 수령 주소\) |
| CELO\_VALIDATOR\_GROUP\_RG\_ADDRESS | 검증자 그룹의 `ReleaseGold` 계약 주소 |
| CELO\_VALIDATOR\_RG\_ADDRESS | 검증자의 `ReleaseGold` 계약 주소 |
| CELO\_VALIDATOR\_GROUP\_SIGNER\_ADDRESS | 검증자 그룹 계정으로 인증된 검증자\(그룹\) 서명자 주소 |
| CELO\_VALIDATOR\_GROUP\_SIGNER\_SIGNATURE | 검증자 그룹 서명자 키의 소유 증명 |
| CELO\_VALIDATOR\_SIGNER\_ADDRESS | 검증자 계정에 의해 승인된 검증자 서명자 주소 |
| CELO\_VALIDATOR\_SIGNER\_PUBLIC\_KEY | 검증자 서명자 주소와 연결된 ECDSA 공개 키 |
| CELO\_VALIDATOR\_SIGNER\_SIGNATURE | 검증자 서명자 키의 소유 증명 |
| CELO\_VALIDATOR\_SIGNER\_BLS\_PUBLIC\_KEY | 검증자 인스턴스에 대한 BLS 공개 키 |
| CELO\_VALIDATOR\_SIGNER\_BLS\_SIGNATURE | BLS 공개 키의 소유 증명 |
| CELO\_VALIDATOR\_GROUP\_VOTE\_SIGNER\_ADDRESS | 검증자 그룹 투표 서명자의 주소 |
| CELO\_VALIDATOR\_GROUP\_VOTE\_SIGNER\_PUBLIC\_KEY | 검증자 그룹 투표 서명자 주소와 연결된 ECDSA 공개 키 |
| CELO\_VALIDATOR\_GROUP\_VOTE\_SIGNER\_SIGNATURE | 검증자 그룹 투표 서명자 키의 소유 증명 |
| CELO\_VALIDATOR\_VOTE\_SIGNER\_ADDRESS | 검증자 투표 서명자의 주소 |
| CELO\_VALIDATOR\_VOTE\_SIGNER\_PUBLIC\_KEY | 검증자 투표 서명자 주소와 연결된 ECDSA 공개 키 |
| CELO\_VALIDATOR\_VOTE\_SIGNER\_SIGNATURE | 검증자 투표 서명자 키의 소유 증명 |
| PROXY\_ENODE | 검증자 프록시의 노드 주소 ~~\(What is ENODE?????\)~~ |
| PROXY\_INTERNAL\_IP | \(선택\) 검증자가 프록시와 통신할 수 있는 내부 IP 주소 |
| PROXY\_EXTERNAL\_IP | 프록시의 외부 IP 주소입니다. PROXY\_INTERNAL\_IP가 지정되지 않은 경우 검증자가 프록시와 통신하는 데 사용할 수 있습니다. |
| CELO\_ATTESTATION\_SIGNER\_ADDRESS | 검증자 계정에 의해 승인된 Attestation 서명자의 주소 |
| CELO\_ATTESTATION\_SIGNER\_SIGNATURE | Attestation 서명자 키의 소유 증명 |
| CELO\_ATTESTATION\_SERVICE\_URL | 배포된 Attestation 서비스에 액세스하는 URL |
| METADATA\_URL | Attestation 서비스의 메타데이터 파일에 액세스하는 URL |
| DATABASE\_URL | 데이터베이스에 액세스할 수 있는 URL, 현재 지원되는 것은 `postgres://`, `mysql://`, `sqlite://` 입니다. |
| SMS\_PROVIDERS | 환경을 설정할 공급자들을 쉼표로 구분한 목록으로, Celo는 현재 `nexmo` 및 `twilio`를 지원합니다. |

### 네트워크 배포 시간표

Mainnet의 설정은 새로운 Baklava 네트워크와 유사하며 배포 타임라인은 다음과 같습니다 \(모든 날짜는 변경될 수 있습니다\).

완료 :

* 4/19 00:00 UTC : 제네시스 블록이 배포된 도커 이미지 
* 4/19 - 4/22 : 인프라 설정 
* 4/22 16:00 UTC : 블록 생산 시작 
* 4/22 : Celo 코어 계약 및 `ReleaseGold` 계약 구축 
* 4/27 : 검증자 선거 및 검증자 epoch 보상의 동결 해제를 위한 거버넌스 제안서 제출 
* 5/1 : 거버넌스 제안이 통과될 경우 선거 및 검증자 보상이 가능. \(검증자는 첫 번째 선거를 위해 검증자 그룹에 등록되고 소속되어 있습니다.\)
* 5/14 : 유권자 보상 및 CELO 이전을 활성화하기 위한 거버넌스 제안서 제출 
* 5/18 : RC1이 메인넷으로 선언되고 거버넌스 제안이 통과되면 CELO 전송 활성화

예정 :

* ~ 5/25 : CELO/USD Oracle 구축 
* ~5/31 : 안정성 프로토콜 동결 해제를 위한 거버넌스 제안서 제출 
* ~6/3 : 거버넌스 제안이 통과되면 안정성 프로토콜이 활성화

{% hint style="info" %}
추가적인 상황을 확인하려면 Release Candidate 1 과 Mainnet 네트워크의 [timeline](https://forum.celo.org/t/release-candidate-1-rc1-timeline-and-details/428) 을 참고하세요.
{% endhint %}

