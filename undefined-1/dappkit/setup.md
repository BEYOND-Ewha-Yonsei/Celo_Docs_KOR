# Setup

## 빠른 시작

시작하기 위해 [https://github.com/celo-org/celo-dappkit](https://github.com/celo-org/celo-dappkit)에서 Truffle Box 템플릿을 사용하는 것이 가장 쉽습니다. 이 저장소는 DappKit을 시작하기 위한 "Hello World"예제를 포함하고 있습니다.

## 구성

DappKit 를 설정하고 구성하는 자세한 방법을 알아보세요.

### 설치

새로운 expo 프로젝트를 생성하기 위해서 expo cli를 사용하세요.

```text
npm install expo-cli --global
// or
yarn global add expo-cli

expo init $YOUR_APP_NAME
```

[https://expo.io/learn](https://expo.io/learn)에서 일반적인 expo 설정에 대해 자세히 알아보기.

### Typescript 지

우리는 Typescript의 큰 팬 이므로 당신이 tabs template을 사용한다면 당신은 이 [가이드라인](https://docs.expo.io/versions/latest/guides/typescript/)을 따라 typescript를 지원할 수 있습니다.

### 설정

DappKit를 추가하려면 다음을 실행하세요.

```text
npm install @celo/dappkit
// or
yarn add @celo/dappkit
```

당신은 node 버전 8.13.0 이상이 필요할 것입니다. 

DAppKit의 dependency는 vanilla Expo에서 약간의 조정이 필요합니다. 첫번째로 많은 Node.js 모듈이 필요합니다. 당신은 대부분을 다음 모듈을 사용하여 얻을 수 있습니다.

```text
npm install node-libs-react-native vm-browserify
// or
yarn add node-libs-react-native vm-browserify
```

당신은 다음 metro.config.js 를 당신의 프로젝트 루트에 추가하고 , 관련된 npm 패키지들이 설치 되었는지 확인해야 합니다.

```text
const crypto = require.resolve('crypto-browserify')
const url = require.resolve('url/')
module.exports = {
  resolver: {
    extraNodeModules: {
      crypto,
      url,
      fs: require.resolve('expo-file-system'),
      http: require.resolve('stream-http'),
      https: require.resolve('https-browserify'),
      net: require.resolve('react-native-tcp'),
      os: require.resolve('os-browserify/browser.js'),
      path: require.resolve('path-browserify'),
      stream: require.resolve('readable-stream'),
      vm: require.resolve('vm-browserify')
    }
  }
}
```

이 방법으로 당신은 프로젝트를 빌드할 수 있지만, 일부 종속성은 전역 환경에서 특정 불변을 유발할 수 있습니다. 이를 위해 다음 내용으로 global.ts 파일을 생성한 다음 import './global'  App.js/tsx 파일 상단에 추가 해야 합니다.

```text
export interface Global {
  btoa: any
  self: any
  Buffer: any
  process: any
  location: any
}

declare var global: Global
if (typeof global.self === 'undefined') {
  global.self = global
}
if (typeof btoa === 'undefined') {
  global.btoa = function (str) {
    return new Buffer(str, 'binary').toString('base64')
  }
}

global.Buffer = require('buffer').Buffer
global.process = require('process')
global.location = {
  protocol: 'https',
}
```

당신은 무시할 수있는 두 가지 경고를받을 수도 있습니다. App.js / tsx에서 다음과 같이 노란색 배너로 이를 막을 수 있습니다.

```text
import { YellowBox } from 'react-native'

YellowBox.ignoreWarnings([
  "Warning: The provided value 'moz",
  "Warning: The provided value 'ms-stream",
])
```

