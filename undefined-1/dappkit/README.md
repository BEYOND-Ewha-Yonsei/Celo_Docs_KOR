# DAppKit

DAppKit은 모바일 DApp이 Celo Wallet과 연동하여 트랜잭션에 서명하고 사용자 계정에 접근할 수 있도록 하는 가벼운 기능의 세트입니다. 이는 더 나은 사용자 경험을 제공합니다: DApp들은 키 관리에 대해 걱정할 필요없이 훌륭한 고유의 경험을 제공하는 데에 집중할 수 있습니다. 또한 상태 또는 연결 관리가 필요하지 않아 더 간단한 개발 환을 제공합니다.

DAppKit은 다음 기능을 지원합니다.

* Celo Wallet에서 계정 정보와 전화번호에 대한 접근 허가 요청합니다. 
* Celo Wallet에서 트랜잭션 서명 허가를 요청합니다. 
* Celo를 사용하여 연락처를 찾기 위해[ Identity Protocol](https://docs.celo.org/celo-codebase/protocol/identity)을 이용하여 전화번호를 탐색합니다. 

DAppKit은 현재 React Native를 고려하여 만들어졌지만, Celo에서 모바일 및 웹 DApp를 만드는 개발자에게는 훌륭한 [Expo framework](https://expo.io/)를 여전히 추천합니다. Expo는 매우 쉬운 설정, 핫 리로딩 등과 같은 멋진 기능을 제공합니다. 현재 대부분의 튜토리얼과 예제는 Expo를 포함하고 있지만 우리는 다른 앱 프레임 워크에 대한 추가 문서를 만드는 작업도 진행 중입니다. 특히 DAppKit은 모바일 앱용으로 설계되었지만 1.1.0-beta.1버전부터 모바일 장치의 브라우저에서 실행되는 웹 DApp에 대한 베타 지원도 제공합니다. 이에 대한 자세한 내용은 아래 Usage 섹션에 포함되어 있습니다.

