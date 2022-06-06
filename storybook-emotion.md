---
description: React 개발자 채용 공고에 자주 보이는 Storybook, emotion에 대하여
---

# Storybook, emotion

### Storybook?

* 컴포넌트 단위의 UI 개발 환경을 지원하는 도
* 컴포넌트의 문서화 도구로도 사용 가능
* React, Vue, Angular 등 지원

### React에 적용

#### Webpack 환경을 구성하지 않고 CRA를 이용하여 적용하는 방법

* 아래 명령어를 통해 typescript 기반의 프로젝트 생성

```javascript
npx create-react-app storybook-app --template typescript
```

* 아래 명령어로 프로젝트가 제대로 생성 되었는지 확인

```javascript
npm run start
```

* 이후 아래의 명령어로 설치

```
npx -p @storybook/cli sb init
```

#### Webpack5로 구성된 프로젝트에 적용하는 방법

* 아래의 명령어로 storybook 설치

```javascript
npx sb init --builder webpack5
```

* dotenv-webpack이 설치되어있지 않으면 해당 패키지도 설치해야 함

```javascript
npm install dotenv-webpack --save-dev
```

#### 실행

* 설치가 되어 있다면 stories directory에 샘플 코드가 생성 되고 package.json에 storybook 실행을 위한 scirpt가 추가됨

```javascript
"scripts": {
    "storybook": "start-storybook -p 6006 -s public",
    "build-storybook": "build-storybook -s public"
},
```

* 제대로 실행이 되어 있는지 확인해보기 위해 아래 명령어로 실행

```javascript
npm run storybook
```

* storybook은 기존의 어플리케이션과 따로 구동되어 어플리케이션을 실행하지 않아도 실행 가능
* 정상 실행이 되면 아래 그림과 같은 웹 페이지가 나타남

![storybook init page](<.gitbook/assets/storybook init.png>)

### Emotion?

* css-in-js의 종류 중 하나로 js 안에서 스타일을 작성할 수 있게 해줌
* 주로 framework agnositc과 react 두 가지 방식으로 사용됨

### Emotion의 장점

* css-in-js 형식으로 스타일을 사용할 수 있음
* class name이 자동으로 부여되기 때문에 스타일이 겹칠 염려가 없음
* 재사용 가능
* props, 조건 등에 따라 스타일 지정 가능
* vendor-prefixing, nested selectors, media queries 등이 적용되어 작성이 간편함
* styled component 사용 방식과 css prop 기능을 지원하여 확장에 용이함
* styled component보다 파일 사이즈가 작고 server side rendering 시 서버 작업이 필요 없음

### Emotion 설치

* 아래의 명령어로 요구에 따른 emotion 설치

```javascript
# Framework Agnostic
npm install @emotion/css

# React
npm install @emotion/react
```

* emotion을 통해 styled-components, nested, media-query 등을 적용 할 수 있음
