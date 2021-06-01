# Overview

이 섹션은 개발자가 Celo에서 응용 프로그램을 빌드하는 데 도움이 되는 몇 가지 주요 도구 및 리소스에 대한 정보를 포함하고 있습니다.

## 빠른 시작 가이

[개발자 코드 예제 페이지](https://d.docs.live.net/developer-guide/start) 안내된 코딩 연습으로 Celo SDK사용을 시작 보세요.

## Tools

### SDKs

* [ContractKit](https://d.docs.live.net/developer-guide/contractkit)
  * Celo 블록체인 유틸리티의 Javascript 패키
  * Celo 블록체 및 계정들의 연결을 관리, 트랜잭션 전송, 스마트 컨트랙트와 상호작용등
  * 거버넌스, 밸리데이터, on-chain 교환 등과 관련된 컨트랙트와 쉽게 연결할 수 있도록 핵심 프로토콜 스마트 컨트랙트를 둘러싼 래퍼 세트 
  * [Web3.js](https://web3js.readthedocs.io/en/v1.2.4/) 포함
* [Celo Ethers.js Wrapper](https://github.com/celo-tools/celo-ethers-wrapper) \(시험\) 
  *  [ethers.js](https://docs.ethers.io/v5/)와 Celo 네트워크를 호환하기 위한 최소한의 래퍼
* [use-contractkit](https://github.com/celo-tools/use-contractkit)
  *  A [Web3Modal](https://web3modal.com/) - ContractKit 웹 기반 어플에 주입하는 경험 - 기반 어플리케이션. Valora, Ledger, Metamask \(Celo 호환 포크\)에 국한되지 않고 모든 WalletConnect 호환 지갑을 포함한 다양한 지갑들을 지원 
* [DappKit](https://d.docs.live.net/developer-guide/dappkit)
  * 당신의 React Native 모바일 어플리케이션 [Valora](http://valoraapp.com/) 지갑을 쉽게 연결 
  * Valora는 사용자 계정, 개인키, 트랜잭션 서명을 관리하여, 당신의 Dapp 빌드에만 집중할 수 있음. 
  * [Dappkit truffle box](https://github.com/critesjosh/celo-dappkit)에서 코드를 확인하고 자세히 알아보기.
* [Python SDK](https://github.com/blaize-tech/celo-sdk-py)
* [Java SDK](https://github.com/blaize-tech/celo-sdk-java)

### Infrastructure

* [Valora](https://valoraapp.com/)
  * 사용자들이 트랜잭션을 보내고 스마트 컨트랙트와 상호작용 할 수 있는 깔끔하고 직관적인 UI를 제
* [Forno](https://d.docs.live.net/developer-guide/forno)
  * 노드 인프라를 운영하지 않고 당신의 dapp을 셀로 블록체인에 연결 할 수 있게 해주는 노드 접근 서비스
* [ODIS](https://d.docs.live.net/developer-guide/contractkit/odis)
  * 잊기 쉬운\(?\) 탈중앙화 신원증명 서비스 
  * 암호화폐를 전화번호로 쉽게 보낼 수 있는 가벼운 신원 레이어 
* Blockscout 블록 탐색 
  * [Alfajores testnet](http://alfajores-blockscout.celo-testnet.org/) & [mainnet](http://explorer.celo.org/)
* [Stats.celo.org ](http://stats.celo.org/)에서 네트워크 활동과 상태를 체크하세요.

#### Networks

* [Alfajores Testnet](https://d.docs.live.net/getting-started/alfajores-testnet)
  * 무료 테스트넷의 CELO와 cUSD [Faucet](https://celo.org/developers/faucet)
  * [Frono](https://d.docs.live.net/developer-guide/forno)가 alfajores연결을 지원합니다. 
  * 모바일 장치 테스트에 Alfajores Celo wallet이 필요합니다.\([support@clabs.co](mailto:support@clabs.co)로 요청하세요.\) 
* 밸리데이터와 프로토콜 변화 테스트를 위한 [Baklava testnet](https://d.docs.live.net/getting-started/baklava-testnet) 

### Ethereum Tools

* Celo와 Ethereum의 유사성은 당신이 인기있는 많은 Ethereum 개발도구들을 사용할 수 있음을 의미합니다.
  * Celo는 EVM을 지원하므로 Solidity \(또는 EVM 바이트 코드로 컴파일되는 모든 언어\)로 스마트 컨트랙트를 작성하는 도구는 Celo와 호환됩니다.
  * ERC20, NFT \(ERC721\) 및 기타 스마트 컨트랙트 인터페이스 표준이 지원됩니다. [Celo for Ethereum Developers](https://d.docs.live.net/developer-guide/celo-for-eth-devs)를 참조하세요
  * [Truffle](https://www.trufflesuite.com/)
  * [OpenZeppelin](https://openzeppelin.com/)
  * [Remix](https://remix.ethereum.org/)
  * Many more

### 진행중인 프로젝

* [Community projects](https://d.docs.live.net/developer-guide/celo-dapp-gallery) 
* [Grant recipients](https://celo.org/experience/grants/directory)
* Web wallets
  * [celowallet.app](https://celowallet.app/)
  * [Celo Terminal ](https://github.com/zviadm/celoterminal/)

## Community

* [Discord](https://chat.celo.org/) 참여하세요.
* [Discourse Forum](https://forum.celo.org/)



