---
description: ES 6 에서 ES 5와의 차이점 분석
---

# ES 6 와 ES 5 의 차이점

### ES ?

* ECMAScript의 약자로 기능이 모든 브라우저에서 동일하게 동작하지 않는 크로스 브라우징 이슈를 해결하기 위해 js를 표준화 한 것

### ES6 와 ES5의 차이

* 변수 선언
  * ES5에는 var 만 있으며 var은 재할당과 재선언에 자유로우며 호이스팅 문제가 있음
  * ES6에는 호이스팅 문제를 해결하기 위해 let, const가 있음\
    let은 한번 선언된 변수의 이름과 동일 이름으로 선언 할수 없고, 값은 재할당 가능함\
    const는 재할당, 재선언 모두 불가함
* 화살표 함수
  * 화살표 함수는 ES6부터 등장함
* 템플릿 리터럴
  * ES6 부터 등장하여 백틱(\`)으로 문자열을 감싸 표현하는 기능

```javascript
// ES5
var name = "이름"
var age = "31"
console.log("이름은" + name + "이고 나이는" + age + "입니다.")
```

```javascript
// ES6
let name = "이름"
let age = "31"
console.log (`나이는 ${name}이고 나이는 ${age} 입니다.`)
```

* Default parameter

```javascript
// ES5
var person = function(name) {
    var name = name || "이름"
    return name
}
```

```javascript
// ES6
let person = function(name="이름") {
    return name
}
```

* Class
  * ES6부터 Class 키워드 사용 가능함

```javascript
// ES5, 프로토타입 기반
var Add = function(arg1, arg2) {
    this.arg1 = arg1
    this.arg2 = arg2
}
Add.prototype.calc = function() {
    return this.arg1 + "+" + this.arg2 + "=" + (this.arg1 + this.arg2)
}
var num = new Add(1, 2)
console.log(num.calc())
```

```javascript
// ES6
class Add {
    constructor(arg1, arg2) {
        this.arg1 = arg1
        this.arg2 = arg2
    }
    calc() {
        return this.arg1 + "+" + this.arg2 + "=" + (this.arg1 + this.arg2)
    }
}
let num = Add(1,2)
console.log(num.calc())
```

* 참고 : [https://velog.io/@weffa/JavaScript-ES5%EC%99%80-ES6-%EC%B0%A8%EC%9D%B4](https://velog.io/@weffa/JavaScript-ES5%EC%99%80-ES6-%EC%B0%A8%EC%9D%B4)

