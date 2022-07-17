# 상속과 프로토타입

### 상속 & 프로토타입?

* Java나 C++과 같이 class 기반의 언어와는 달리 js는 동적인 언어이며 class 가 없음 ( es2015부터 class 키워드를 지원하기 시작했으나, 이는 JAVA나 C++ 과는 다르며 js 는 프로토타입 기반의 언어임 )
* 상속 관점에서 js의 유일한 생성자는 객체 뿐임
* 각각의 객체는 \[\[Prototype]]라는 private 속성을 가지는데 자신의 프로토타입이 되는 다른 객체를 가리킴\
  해당 객체의 프로토타입 또한 프로토타입을 가지고 있으며 이를 반복하다 null을 프로토타입으로 가지는 object에서 끝나게 됨\
  null은 더 이상의 프로토타입이 없다고 정의되며, 프로토타입 체인의 종점 역할을 함
* 프로토타입적 상속 모델은 고전적인 방법보다 좀 더 강력한 방법임

### 프로토타입 체인을 이용한 상속

#### 속성 상속

* js 객체는 속성을 저장하는 동적인 속성과 프로토타입 객체에 대한 링크를 가짐
* 객체의 어떤 속성에 접근하려 할 때 그 객체 자체 속성 뿐만 아니라 객체의 프로토타입 부터 시작하여 종단에 이를 때 까지 속성을 탐색함
* 객체의 속성에 값을 지정하면 '자기만의 속성'이 생김. 단, getter & setter가 적용되는 속성이 상속되는 경우 예외적인 규칙이 적용됨

#### Method 상속

* js에 method라는 것은 없음. 하지만 js는 객체의 속성으로 함수가 지정 가능하고 속성 값을 사용하듯 쓸 수 있음
* 속성 값으로 지정한 함수의 상속 역시 위에서 본 속성의 상속과 동일함
* 상속된 함수가 실행될 때, this라는 변수는 상된오즈젝트를 가리킴. 그 함수가 프로토타입의 속성으로 진행 되었다고 해도 무방함.
* 싱속된 함수가 실행 될 때 this라는 변수는 상속된 오브젝트를 가르킴. 그 함수가 프로토타입의 속성으로 지정외었다고 해도 마찬가지임

### JS에서 프로토타입 사용 방법

* js 에서 함수는 속성을 가질 수 있음
* 모든 함수에는 prototype이라는 특수한 속성이 있음
* prototype.foo = 'bar' 선언과 같은 방법으로 속성을 추가 할 수 있음

### 객체를 생성하는 여러 방법과 프로토타입 체인 결과

#### 문법 생성자로 객체 생성

```javascript
var o = {a: 1};
// o 객체는 프로토타입으로 Object.prototyp[e 을가짐
// 이로 인해 o.hasOwnProperty('a')와 같은 코드를 사용할 수 잇음
// Ojbect.prototype 의 프로토타입은 null 임
// O ---> Object.prototype ---> null

var a = ['a', 'b', 'c'];
// Array.prototype을 상속받은 배열도 마찬가지임
// indexOf, forEach 등의 메소드를 가짐
// 프로토타입 체인은 a ---> Array.prototype ---> Object.prototype ---> null

function f() {
    return 2;
}
// 함수는 Function.prototype을 상속받음
// call, bind와 같은 메소드를 가짐
// 프로토타입 체인은 f ---> Function.prototype ---> Object.prototype ---> null
```

#### 생성자를 이용

* js 에서 생성자는 단지 new 연산자를 사용해 함수를 호출하면 됨
* ECMAScript 5 에서는 Object.create라는 메소드를 호출하여 새로운 객체를 만들 수 있음
* 생성된 객체의 프로토타입은 이 메소드의 첫 번째 인수로 지정됨

```javascript
var a = {a: 1}
// a ---> Object.prototype ---> null

var b = Object.create(a);
// b --> a ---> Object.prototype ---> null

var c = Object.create(b);
// c ---> b ---> a ---> Object.prototype ---> null

var d = Object.create(null);
// d ---> null
```

#### Class 키워드 이용

* ECMAScript 2015에서는 class를 구현하였으나 동작방식이 객체지향 언어의 class와는 다름
* js는 여전히 프로토타입 기반의 언어
* 새로 도입된 키워드는 class, constructor, static, extends, super가 있음

#### 성능

* 프로토타입은 체인에 걸친 속성 검색으로 성능에 부정적 영향을 줄 수 있으며 때로는 치명적일 수 있음
* 존재하지 않는 속성에 접근하려는 시도는 항상 모든 프로토타입 체인인 전체를 탐색해서 확인하게 만듬
* 객체의 속성에 걸쳐 루프를 수행하는 경우 프로토타입 체인 전체의 모든 열거자 속성에 대해 적용됨
* 객체 개인 속성인지 프로토타입 체인상 어딘가에 있는지 확인하기 위해서는 Object.prototype에서 모든 Object로 상속된 hasOwnProperty 메소드를 이용해야 함

#### 좋지 않은 사례 : 기본 프로토타입의 확장 변형

* Object.prototype 혹은 빌트인 프로토타입의 확장은 종종 이용되지만 오용임
* 이 기법은 Monkey pathcing으로 불리며 캡슐화를 망가뜨림
* Prototype.js와 같은 유명한 프레임워크에서도 사용되지만, 빌트인 타입에 비표준 기능을 추가하는 것은 좋은 생각이 아님
* 유일하게 좋은 사용 예라면, 새로운 js 엔진에 Array.forEach등의 새로운 기능을 추가하면서 빓트인 프로토타입을 확장하는 정도임

### Prototype 그리고 Object.getPrototypeOf

* Java나 C++에 익숙한 개발자는 class가 없고 모든 것이 동적이고 실행 시 결정되는 js 특징 때문에 어려움을 겪을 수도 있음
* 모든 것은 객체이고, 심지어 class를 흉내내는 방식도 단지 함수 오브젝트를 이용하는 것임

### 프로토타입 상속의 종류

* 프로토타입 상속에는 위임형 상속, 연결형 상속, 함수형 상속 총 3가지가 있음

#### 위임형 상속 (Delegation inheritance)

* 위임형 상속에서 프로토타입 객체는 다른 객체의 기반이 됨
* 위임 프로토타입을 상속받을 경우 새 객체는 해당 프로토타입에 대한 참조를 가지고 있음
* 새 객체의 속성에 접근할 때 해당 객체가 직접적으로 속성을 소유하고 있는지 먼처 체크함
* 없다면 다음 순서로 \[\[Prototype]]을 체크함. 이 과정은 프로토타입 체인을 따라서 모든 객체의 프로토타입 체인의 최상위에 있는 객체인 Object.prototype에 도달할 때 까지 반복함
* 메소드를 위임 상속할 경우 모든 객체가 각 메소드에 대해 하나의 코드를 공유하므로 메모리를 절약할 수 있음
* js에서 이를 구현하는 방법은 여러가지가 있는데 ES6에서는 아래 예시와 같은 방식이 많이 사용 됨

```javascript
class Greeter {
    constructor (name) {
        this.name = name || 'John Doe';
    }
    hello () {
        return `Hello, my name is ${this.name}`;
    }
}

const george = new Greeter('George')
const msg = george.hello();
console.log(msg); // Hello, my name is George
```

* Object.create(null)을 통해 프로토타입을 null로 지정하여 속성 위임 없이 객체를 생성할 수 있음
* 이 방법의 큰 단점 중 하나는 상태를 저장하는데 좋은 방법이 아님. 객체나 배열의 상태를 변경하게 되면 같은 프로토타입을 공유하는 모든 객체의 상태가 변경됨
* 상태 변경이 전파되는 것을 막으려면 각 객체마다 상태 값의 복사본을 만들어야 함

#### 연결형 상속 (Concatenative inheritance)

* 연결형 상속은 한 객체의 속성을 다른 객체에 모두 복사함으로써 상속을 구현하는 방법임
* 이 상속법은 js 객체의 동적 확장성을 이용한 방법임
* 객체 복사는 속성의 초기값을 저장히기 위한 좋은 방법임. 이 방법은 Object.assign()을 통해 구현하는 것이 보통이며 ES6 이전에 Lodash, Underscore, jQuery 등의 library 등의 .extend() 와 비슷한 메소드로 제공한 방법임

```javascript
const proto = {
    hello: function hello() [
        return `Hello, my name is ${this.name}`;
    }
};

const george = Object.assign({}, proto, {name: 'George'});
const msg = george.hello();
console.log(msg); // Hello, my name is George
```

* 연결형 상속은 좋은 방법이며 클로져와 같이 사용한다면 훨씬 효과적인 상속 방식임

#### 함수형 상속 (Functional inheritance)

* 함수형 상속이라는 단어는 Douglas Crockford가 자신의 저서 'Javascript: The Good Parts"에서 창조한 단어임
* 이 방법은 새 속성들을 연결형 상속으로 쌓되 상속 기능을 Factory 함수로 만들어 사용하는 방식임
* 기존의 객체를 확장하는데 쓰이는 함수를 일반적으로 믹스인 함수라고 칭함. 객체 확장에 함수를 사용하는 가장 큰 이점은 Private Data를 클로져를 통해 캡슐화를 시킬수 있다는 점임. 다르게 말하면 Private 상태를 지정할 수 있음
* 특정 함수를 통할 필요 없이 public 접근이 가능한 속성에 대해 접근 제한을 거는 것은 문제가 있음. 따라서 private 클로져에 속성 값을 숨겨야 하며 이는 아래 예시와 같이 구현함

```javascript
const rawMixin = function () {
    const attrs = {};
    return Object.assign(this, {
        set (name, value) {
            attrs[name] = value;
            this.emit('change', {
                prop: name,
                value: value
            });
        },
        get (name) {
            return attrs[name];
        }
    }, Events.prototype);
};

const mixinModel = (target) => rawMixin.call(target);
const george = {name : 'george' };
const model = mixinModel(george);
model.on('change', data => console.log(data));
model.set('name', 'Sam');

/*
{
    prop: 'name',
    value: 'Sam'
}
*/
```

* attrs 을 public 속성에서 private 영역으로 옮겨서 public API를 통한 접근을 차단할 수 있음
* 접근할 수 있는 유일한 방법은 Privileged 메소드 뿐임. Privilieged 메소드는 클로져 영역에 정의된 함수로 private data에 접근 가능한 함수들을 말함
* 위의 예제에서는 믹스인 함수 rawMixin() 에 대한 wrapper로 mixinModel() 을 선언 한 것을 알 수 있음. 이는 예제에서 Function.prototype.call()을 사용했듯이 함수 내에서 this의 값을 설정해야 하기 때문임. Wrapper를 생략하고 호출자가 알아서 하도록 놔둘 수 있지만 그럴 경우 혼동될 가능성이 있음
* 참고: [https://developer.mozilla.org/ko/docs/Web/JavaScript/Inheritance\_and\_the\_prototype\_chain](https://developer.mozilla.org/ko/docs/Web/JavaScript/Inheritance\_and\_the\_prototype\_chain)

