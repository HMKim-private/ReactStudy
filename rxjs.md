---
description: >-
  해당 페이지는 RxJS에 대해 다룸 (출처 :
  https://pks2974.medium.com/rxjs-%EA%B0%84%EB%8B%A8%EC%A0%95%EB%A6%AC-41f67c37e028)
---

# RXJS

### RxJS?

* RxJS는 Reactive Extensions For JavaScript 라이브러리
* 여기서 Reactive Extensions는 ReactiveX 프로젝트에서 출발한 Reactive 프로그래밍을 지원하기 위해 확장했다는 뜻임
* RxJS는 event stream을 observable이라는 객체로 표현한 후 비동기 이벤트 기반의 소스코드 작성을 도움
* 이벤트 처리를 위한 api로 다양한 연산자를 제공하는 함수형 프로그래밍 기법이 도입되어 있음

### Reactive 프로그래밍?

* Reactive 프로그래밍이란 이벤트나 배열 같은 data stream을 비동기로 처리해 변화에 유연하게 반응하는 프로그래밍 패러다임
* 외부와 통신하는 방식은 pull과 push 시나리오가 있음
  * pull 시나리오
    * 외부에서 명령하여 응답하고 처리함
    * 데이터를 가지고 오기 위해서 계속 호출 해야 함
  * push 시나리오
    * 외부에서 명령하고 기다리지 않고, 응답을 수신하면 반응하여 처리함
    * 데이터를 가지고 오기 위해 구독해야 함
* Reactive 프로그래밍은 push 시나리오를 채택함
* 비동기 코드가 많아지면 제어의 흐름이 복잡하여 소스코드의 로직 분석이 어려워짐
* RxJS는 Javascript의 비동기 프로그래밍의 문제를 해결하는데 도움을 줌
* RxJS는 Observer 패턴을 적용한 Observable이라는 객체를 중심으로 동작함

### RxJS Observable

* Observable은 특정 객체를 관찰하는 Observer에게 여러 이벤트나 값을 보내는 역할을 함
* Observer에는 3가지 method가 존재함
  * next: Observable 구독자에게 데이터를 전달함
  * complete: Observable 구독자에게 완료 되었음을 알림. next는 더이상 데이터를 전달하지 않음
  * errir: Observable 구독자에게 에러를 전달함. 이후 next및 complete 이벤트가 발생하지 않음

### RxJS Observable Lifecycle

* 생성(Observable.create())
  * 생성 시점에는 어떠한 이벤트도 발생되지 않음
* 구독(Observable.subscribe())
  * 구독 시점에 이벤트를 구독할 수 있음
* 실행(Observer.next())
  * 실행시점에 이벤트를 구독하고 있는 대상에게 값을 전달함
* 구독 해제(observer.complete(), osbservable.unsubscribe())
  * 구독 해제 시점에 구독하고 있는 모든 대상의 구독을 종료함

### RxJS Subject

* RxJS에는 Subject를 지원함
* Subject는 여러 Observer에서 구독이 가능하며, Subject에서 전달하는 값을 Observer들이 전달받음

### RxJS Scheduler

* RxJS에서는 Scheduler를 지원함
* js는 싱글스레드, 이벤트 루프로 동작하기 때문에, RxJS에서의 Scheduler는 이벤트 루프에 어떤 순서로 처리될지로 구현됨
* Scheduler는 3가지 종류가 존재함
  * AsyncScheduler
    * setTimeout과 유사함
    * asyncScheduler.schedule(()  => console..log('async), 3000);
  * AsapScheduler
    * asapScheduler.schedule(() => console.log('asap'));
    * 다음 이벤트 루프에 실행
  * QueueScheduler
    * Scheduler에 전달된 state를 처리함

