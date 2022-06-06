---
description: Front-end 개발에 사용되는 MVC,  MVP, MVVM 패턴이란 무엇인가
---

# Design Pattern - 2

Front-end 개발에서 들을 수 있는 MVC, MVP, MVVM 패턴은 앞서 기술한 Design Pattern 중 Observer Pattern에 해당

이때 추가적으로 Mocking이라는 개념의 이해도 요구됨

### Mocking이란?

* 외부 API에 의존하는 단위 테스트 시, 외부 API에 문제가 있을 경우 테스트를 진행하기 힘들다. 이를 고려하여 외부 의존성을 가짜(Mockup)으로 대체하여 테스트하는 기법을 Mocking이라 한다.
* Mocking은 외부 서비스 의존도를 줄이고, 독립 실행하는 단위 테스트 작성을 위해 사용되는 테스트 기법이다.

### MVC Pattern (Model View Controller)

![MVC Pattern](<.gitbook/assets/mvc pattern.png>)

* MVC Pattern은 어플리케이션은 Model, View, Controller로 구성한다.
  * Model: View에 표시하는데 필요한 데이터를 의미함. Model은 비즈니스 로직 (비즈니스 및 데이터 모델)을 설명하는 클래스 모음. 또한 데이터를 변경하고 조작하는 방법으 데이터에 대한 비즈니스 규칙을 정의함
  * View: View는 XML, HTML과 같은 UI 구성 요소를 나타냄. View는 Controller에서 수신받은 데이터를 표시함. View는 상태 변경에 대한 Model을 모니터링하고 업데이트된 Model을 표시함. Model과 View는 Observer Pattern을 사용하여 서로 상호작용함.
  * Controller: Controller는 요청을 처리함. Model을 통해 사용자의 데이터를 처리하고 결과를 View로 전달함. 일반적으로 View와 Model의 중재자 역할을 함.

### MVP Pattern (Model View Presenter)

![MVP Pattern](<.gitbook/assets/mvp pattern.png>)

* MVC Pattern에서 파생되어 Controller 대신 Presenter를 사용함. 이 Pattern은 어플리케이션을 Model, View, Presenter로 나눔
  * Presenter: View를 통해 사용자로 부터 입력 받은 후, Model의 도움을 받아 사용자의 데이터를 처리하고, 결과를 다시 View로 전달함. Presenter는 인터페이스를 통해 View와 통신함.\
    인터페이스는 필요한 데이터를 전달하는 Presenter Class에서 정의됨. View 컴포넌트 요소는 이 인터페이스를 구현하고 원하는 방식으로 데이터를 렌더링함.\
    MVP Pattern에서 Presenter는 Model을 조작하고 View도 업데이트 함. View와 Presenter는 서로 완전히 분리되어, 인터페이스를 통해 통신한다. View의 decoupling mocking이 더 쉽고 MVC Pattern에 대해 MVP Pattern을 활용하는 어플리케이션의 단위 테스트가 더 쉬워짐.

### MVVM Pattern (Model View View-Model)

![MVVP Pattern](<.gitbook/assets/mvvm pattern.png>)

* View와 View-Model 간의 양방향 데이터 바인딩을 지원함. 이를 통해 View-Model 상태 내에서 변경 사항을 View로 자동 전파 할 수 있음. 일반적으로 View Model은 Observer Pattern을 사용하여 View-Model의 변경 사항을 Model에 알림.
  * View-Model: View의 상태를 유지하고 View에 대한 작업의 결과로 Model을 조작하며 View 자체에 이벤트를 트리거하는데 도움이 되는 method, 명령 및 기타 속성을 노출함. View에는 View-Model에 대한 참조가 있지만 View-Model에서는 View에 대한 정보가 없음. View와 View-Model 사이에 N:1 관계가 있다는 것은 많은 View가 하나의 View-Model에 mapping 될 수 있음을 의미. View와 완전히 독립적임.\
    양방향 데이터 바인딩 또는 View와 View-Model 간의 양방향 데이터 바인딩은 View-Model의 Model 및 속성이 View와 동기화 되도록 함. MVVM Pattern은 양방향 데이터 바인딩 지원이 필요한 어플리케이션에 적합함.

