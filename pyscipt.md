---
description: >-
  Web development에 사용되는 Javascript와 Python에 대한 비교(해당 문서는 youtube의 노마드코더 채널에서
  참고함)
---

# PyScipt?

Web development에 많이 사용되어오는 Javascript와 Django, Fast Api등을 통해 Back-end 개발 위주로 사용되어 왔던 Python이 점차적으로 Front-end 개발에도 사용 되어 질 수 있도록 구성되고 있음



### PyScript의 등장

Web development에서 주로 사용되는 언어는 js임. js를 많이 선호한다기 보다는 브라우저가 이해할 수 있는 언어가 오직 js이기 때문.  또한 Vue, React, Angular와 같은 js기반의 강력한 Progressive Framework, libaray 등이 있음.

하지만 최근 Python이  js를 대체 할 수 있는 PyScript가 등장함. [https://pyscript.net/](https://pyscript.net/)\
Python은 back-end, ui 어플리케이션, Data science, AI등 다양한 분야에서 사용되고 있고 관련 커뮤니티의 규모가 큼.\


PyScript는 framework html과 python을 사용하여 다이나믹 어플리케이션을 빌드 할 수 있도록 Anaconda에서 개발됨.&#x20;

PyScript의 사용법은 아래 그림과 같이 body tag 내 py-script tag를 작성하고 내부에 python 코드를 작성하면 됨. 기존 python에서 사용하는 모듈도 import 가능

```html
<body>
    <py-script>
        from datetime import datetime
        print(f"Today is {datetime.now()}")
    </py-script>
</body>
```

또한 py-env tag를 통해 python 파일 및 패키지를 가져 올 수 있음.

```html
<py-env>
    - numpy
    - matplotlib
</py-env>
```

PySciprt는 Pyodide와 WebAssembly로 작동\
Pyodide는 CPython의 포트이며 Python 인터프리터이지만 WebAssembly로 컴파일 된 것. WebAssembly는 프로그래밍 언어가 아니라 컴파일 대상임.

아직 초기 단계라 실험적인 단계임. 안정적이 되기까지는 시간이 걸릴 것으로 보임.
