---
description: Forno
---

# Forno

Forno는 Celo 네트워크와 상호 작용하는 cLabs의 노드 서비스입니다. Forno는 직접 노드를 운영할 필요 없이 Celo 블록체인에 연결할 수 있게 해줍니다.

Forno는 HTTP와 웹 소켓 엔드 포인트\(endpoint\)를 갖고 있으며, 이 엔드 포인트\(endpoint\)를 네트워크에 전파하고 싶은 Celo의 현재 데이터나 지난 트랜션의\(transaction\) 쿼리를 보내는 데에 사용할 수 있습니다. 이 서비스는 non-archive 모드로 풀 노드를 운영하며, 이로 인해 현재 블록체인 상태에 대한 쿼리를 보낼 수는 있지만 블록체인의 이전 상태에는 엑세스할 수 없습니다.

Forno는  [ContractKit](https://docs.celo.org/developer-guide/contractkit)를 이용하여 `Http Provider`로 사용할 수 있습니다.

```javascript
const ContractKit = require('@celo/contractkit')
const kit = ContractKit.newKit('https://alfajores-forno.celo-testnet.org')
```

Forno는 퍼블릭 노드로, 트랜잭션을 보내기 위해서는 트랜잭션을 Forno에 보내기 전에 프라이빗 키로 트랜잭션에 서명을 해야 합니다. 이 [Hello Celo](https://docs.celo.org/developer-guide/start/hellocelo) 가이드에서 Forno를 이용해 Alfajores 테스트넷에 연결하고 트랜잭션에 서명을 하고, 트랜잭션을 네트워크에 보내는 방식을 배울 수 있습니다.

## Forno networks

[이 페이지](https://docs.celo.org/getting-started/choosing-a-network)를 참고하여 자신에게 맞는 네트워크를 찾아보세요.

```javascript
Alfajores = 'https://alfajores-forno.celo-testnet.org' 
            'wss://alfajores-forno.celo-testnet.org/ws' (for websocket support)

Baklava = 'https://baklava-forno.celo-testnet.org'

Mainnet = 'https://forno.celo.org'
          'wss://forno.celo.org/ws' (for websocket support)
```

### 웹 소켓 연결 & 이벤트 리스너

웹 소켓 연결은 스마트 컨트랙트가 보내는 로그\(이벤트\)들을 모니터링 하는 데에 유용하지만, Forno는 웹 소캣 연결을 20분 동안만 허용합니다. 계속 로그\(이벤트\)들을 모니터링하길 원한다면, 연결이 끊어질 때 다시 웹 소켓 엔드 포인트에 연결이 가능합니다. 이벤트 리스너를 적용하고 커넥션이 끊어졌을 때 다시 커넥션을 생성하는 예시 스크립트는 [여기](https://gist.github.com/critesjosh/a230e7b2eb54c8d330ca57db1f6239db)서 보실 수 있습니다.

