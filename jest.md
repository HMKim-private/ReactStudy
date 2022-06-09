---
description: unit test 도구로써 많이 사용되는 Jest에 대하여
---

# Jest

### Jest?

* 코드가 제대로 동작하는지 확인하는 test case를 만드는 testing framework
* lint가 코드 스타일에 rule을 정하는 것이라면 코드가 올바른 기능을 하는지 체크할 수 있음
* 이를 통해 보다 안정적이고 제대로 동작하는 코드 작성 가능함

### JEST 설치 방법

* JEST는 yarn과 npm 모두 설치 가능함

```javascript
// yarn
yarn add --dev jest

//npm
npm install --save-dev jest
```

* package.json 파일을 열고 test script를 jest로 수정함

```javascript
"scripts": {
    "test": "jest"
}
```

* 개별 명령어를 따로 설정해서 원하는 부분의 테스트만 진행 가능함

```javascript
"scripts": {
    "test": "jest",
    "test:1": "jest 1-example/",
    "test:2": "jest 2-review/",
    "test:3": "jest 3-review/",
    "test:watch": "jest --watch",
    "test:circlei": "jest --json --outputFile=.circlei/results.json",
    ...
    }
```

### Jest 구성

* jest는 global function과 matcher로 구성되어 있
* global function은 테스트를 설정하는 function임
* jest는 결과에 따라 다른 matcher를 사용함
* 사용 예는 아래와 같음

```javascript
//sum.js

function (sum a, b) {
    return a + b;
}

module.exports = sum;
```

```javascript
//sum.test.js

const sum = require("./sum");

test("adds 1 + 2 to equal 3", () => {
    expect(sum(1,2)).toBe(3);
    });
```
