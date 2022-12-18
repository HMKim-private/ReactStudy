---
description: 해당 페이지는 https://taenami.tistory.com/132?category=1228183 의 내용을 참고함
---

# Cypress

#### 해당 페이지는 Vue3를 이용하여 FE개발을 진행 하며 단위 테스트의 중요성을 깨닫고 Jest를 이용하려 하는 과정 중 Cypress를 알게 되어 단위테스트 뿐만 아니라 E2E테스트까지 가능한 점을 알게 되어 사용하게 됨

### Cypress?

* javascript E2E 테스트 프레임워크
* cypress를 이용하여 E2E, Integration tests, Unit testf를 할 수 있음

### Cypress 특징

* Cypress Test Runner를 설치하고 로컬에서 테스트 작성
* CI 테스트 구축 및 결과 기록
* Cypress는 테스트가 실행될 때 스냅샷을 만듦. 각 단계에서 정확히 어떤 일이 발생했는지 확인 할 수 있음
* Chrome Devtool과 같은 익숙한 도구에서 빠르게 직접 디버깅할 수 있음 (여러 브라우저 환경 지원)
* 테스트를 변경할 때마다 자동으로 다시 로드함

### Cypress의 특장점

#### Architecture

* Selenium과 같은 대부분의 테스트 도구는 브라우저 실행하고 네트워크를 통해 원격 명령을 실행하여 작동하는 것과 달리 Cypress는 애플리캐이션과 동일한 환경에서 실행 됨
* Cypress는 Node위에 동작하는 서버를 띄우게 됨. 실제 브라우저에서 테스트 진행
* 궁극적으로 전체 자동화 프로세스를 제어하므로 브라우저 안팎에서 일어나는 모든 일을 이해할 수 있기 때문에 Cypress가 다른 어떤 도구보다 일관된 결과를 제공할 수 있음

#### Native access

* 응용 프로그램 내에서 작동하므로 document, window, DOM 요소, 응용프로그램 인스턴스, 함수, 타이머 등 Cypress 테스트 할 때 접근할 수 있음

#### Debuggability

* Cypress는 사용성을 위해 제작됨
* 애플리케이션의 스냅샷을 만들고 명령이 실행되었을 때의 상태를 볼 수 있도록 함
* 테스트가 실행되는 동안 개발자 도구를 사용할 수 있으며 모든 console 메시지, 모든 네트워크 요청을 볼 수 있음

#### Cypress Test Types

* E2E
  * Cypress는 브라우저에서 실행되는 모든 항목에 대해 E2E테스트를 실행하도록 설계 됨
  * 일반적으로 E2E 테스트는 브라우저에서 App을 방문하고 실제 User를 UI를 통해 작업 수행함

```javascript
it('cypress tests', () => {
    cy.visit('https://localhost')
    cy.get('.new-input').type('write code{enter}')
        .type('write tests{enter}')
    cy.get('li.todo').should('have.length',2)
})
```

* Component
  * Cypress를 사용하여 일부 web framework에서 Component tests를 실행할 수도 있음(필자는 vue3를 사용함)

```javascript
import { mount } from @cypress/vue
import TodoList from './components/TodoList'

it('contain the correct number of todos', () => {
    const todos = [
        { text: 'Buy milk', id: 1 },
        { text: 'Learn E2E testing', id: 2 },
    ]
    
    mount(<TodoList todos={todos} />)
    cy.get('[data-testid=todos]')
            .should('have.length', todo.length)
})
```

* API
  * Cypress는 임의의 HTTP 호출을 수행할 수 있으므로 API 테스트에 사용할 수 있음

```javascript
it('adds a todo', () => {
    cy.request({{
        url: '/todos',
        method: 'POST',
        body: {
            title: 'Write REST API',
        },
    })
        .its('body')
        .should('deep.contain', {
            title: 'Write REST API',
            completed: false,
        })
})
```

