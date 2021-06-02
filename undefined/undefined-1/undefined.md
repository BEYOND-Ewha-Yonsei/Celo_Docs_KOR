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

### 필요 조건

#### Staking 요구조건

셀로는 [지분 증명](../celo-codebase/protocol/proof-of-stake) 합의 메커니즘을 사용하므로 검증자가 블록 생산에 참여하기 위해서는 CELO를 보유하고 있어야 합니다. 현재는 검증자를 등록하는 데 10,000 CELO, 검증자 그룹을 등록하는 데에는 멤버당 10,000 CELO 가 요구됩니다.

필요한 CELO가 없는 경우 [Baklava에서 검증자 실행](running-a-validator-in-baklava.md)에 따라 Baklava 네트워크에서 검증자를 생성하는 프로세스를 시도할 수 있습니다.

여기서는 CELO 보유 유무에 대해 논의하지 않겠지만 필요한 CELO를 보유하고 있다는 것이 전제 조건이며, 이 가이드에서 사용자의 자금은 검증자와 검증자 그룹에 대한 두 가지 `ReleaseGold` 계약으로 보관된다고 가정합니다. 만약 그렇지 않은 경우 여기서 제공된 명령어를 조정해야 하지만 가이드는 여전히 필요한 단계를 제공할 것 입니다.





