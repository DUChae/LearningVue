# Learning-Vue.js

<details>
  <summary>Vue.js 소개</summary>

# Vue.js란?

- 간단한 화면 UI 개발부터 라우팅, SSR 등의 애플리케이션 레벨의 개발을 지원하는 프레임워크
- 리액트와 더불어 실무에서 가장 많이 사용되고 있는 프론트엔드 개발 라이브러리
- 리액트에 비해 진입 장벽이 낮고 쉽게 배울 수 있다.
- 개발 생산성이 높고 자바스크립트 지식이 크게 요구되지 않는다.
- 프론트엔드, 백엔드 등 점차 직무적으로 전문화되고 있는 상황에서 처음 개발을 시작하는 프론트엔드 개발자 또는 백엔드 개발자에게 선호되는 경향

# Vue 2와 Vue 3의 차이점

- 라이브러리 내부 로직 재작성
- 주요 개발 도구들 변경
  - 예) 뷰 개발자 도구, VSCode 플러그인, Vite 기반 프로젝트 생성 등
- 컴포지션 API, Teleport 등 새로운 문법 지원
- 리액티비티 시스템 기반 API 변경
- 공식 문서 변경

# Vue 3의 코드 작성 방식

## 옵션 API

```jsx
<div id="app">{{message}}</div>
<script>
	Vue.createApp({
		data(){
			return {
				message: 'hi',
				};
			},
		}).mount('#app');
</script>
```

## 컴포지션 API

```jsx
<div id="app">{{message}}</div>
<script>
	Vue.createApp({
		setup(){
			const message=ref('hi');
			return {
				message
				}
			},
		}).mount('#app');
</script>
```

- Vue 3에서는 옵션 API 와 컴포지션 API 모두 작성할 수 있습니다.
- 초급자들은 옵션 API
- 고급자들은 컴포지션 API

# Hello World (Vue.js 인스턴스)

```jsx
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<!-- vue관련 라이브러리를 파일 안에서 사용할 수 있도록 라이브러리 CDN링크를 갖고오겠음 -->
<!-- CDN(Content Delivery Network)는 vue.js파일을 어딘가에 배포를 해놓고 빠르게 접근할 수 있게 링크 제공하는 것 -->

<div id="app">{{message}}</div>
<!-- message라는 것은 Vue안에 있는 데이터를 연결하여 화면에 표기하겠다는 의미함 -->

<script>
  Vue.createApp({
    data() {
      return {
        message: 'Hello Vue 3!'
      }
    }
  }).mount('#app')
	//vue를 사용할 인스턴스를 만들고, 인스턴스를 화면에 붙임
  //mount는 인스턴스를 화면에 붙이는 역할을 함
  //mount안에 있는 #app은 id가 app인 태그를 의미하며 div태그를 의미함
</script>
```

- 첫 시작은 `<div id="app"></div>` 를 작성하며 시작
- `<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>` : vue관련 라이브러리를 파일 안에서 사용할 수 있도록 라이브러리 CDN링크를 갖고오겠다는 의미입니다.
  - 이는 CDN으로써 `CDN`(Content Delivery Network)는 vue.js파일을 어딘가에 배포를 해놓고 빠르게 접근할 수 있게 링크 제공하는 것입니다.
- 그리고 본문인 `script 태그`를 보면 vue를 사용할 인스턴스를 만들고, 인스턴스를 화면에 붙입니다. `mount`는 인스턴스를 화면에 붙이는 역할을 하며 mount안에 있는 `#app`은 `id`가 `app`인 태그를 의미하며 `div태그`를 의미합니다.
- `div태그` 안에 `message`를 넣으며 화면에 표기합니다.

![Untitled](Vue%20js%20592c21c9ddc04157bf5095a04490ac0c/Untitled.png)

- 위 사진에서 message의 값을 바꿀 수 있는데, 이는 데이터의 변화에 따라 화면의 UI 값이 바뀌는 것이 `vue`에서 추구하는 `리액티비티`입니다.
</details>

<details>
<summary>Vue.js 핵심 동작 원리</summary>

리액티비티의 예를 소개한 위의 내용과 같이 데이터를 변경하면 화면이 변경되고 있었습니다. 이러한 동작은 내부 구현이 어떻게 되었는지 이해하면 도움이 되기에 간단히 구현해보겠습니다.

vue 3폴더를 만든 후, reactivity.html파일을 만들었습니다.

```jsx
<div id="app"></div>

<script>
  const data = {
    a: 10
  }
  const app = new Proxy(data, {
    get() {
      console.log('hi')
    }
  })
</script>
```

![Untitled 1](https://github.com/DUChae/LearningVue/assets/97602018/a6087d2b-1618-43f9-b1d4-6611bae9b88b)

- data 객체 생성
- proxy constructor 생성, 첫번째 인자로 data를 전달하며 data를 감시하고 있다가 변화가 있으면 알려줌
- 두번째 인자로 data를 정의하는 객체를 전달
- Data라는 동작을 모방하는 무언가를 만들겠다는 것
- data와 app은 동일한 객체를 가리키고 있으며 같은 결과를 보여줌, get의 내용이 바뀌면 Data의 내용도 바뀜
- new Proxy라는 것이 data라는 객체를 모방한 다음 동작을 추가했다고 보면되는데 get은 data라는 객체의 속성을 접근할 때마다 출력할 내용이라고 보면 됨
- data의 객체의 속성을 설정한다면 어떤 동작을 지정해볼 수 있을 것같은데 set으로 지정해보겠음

```jsx
<div id="app"></div>

<script>
  const data = {
    a: 10
  }

  const app = new Proxy(data, {
    get() {
      console.log('값 접근')
    },

    set() {
      console.log('값 갱신')
    }
  })
</script>
```

![Untitled 2](https://github.com/DUChae/LearningVue/assets/97602018/bb66b3af-ddf0-4bfd-9755-3b1523577c25)

- proxy를 통해 data의 속성을 접근하면 get의 내용이 출력되고, data의 속성을 갱신하면 set의 내용이 출력됨
- 객체의 동작을 정의할 수 있고 추가적으로 지정할 수 있음

# 동작 원리 구현

위에서 proxy에 대해 get , set을 정의했었기 때문에 set하는 동작을 가지고 data의 a의 값이 변경되었을 때 그 값을 이용하여 화면에 출력하는 것을 해보겠습니다.

```jsx
<div id="app">
  <!-- 여기에 뭔가 렌더링 된다.
    렌더링 : 화면에 무언가를 표시하는 행위
    -->
</div>

<script>
  const data = {
    message: 10
  }
  function render(sth) {
    const div = document.querySelector('#app')
    div.innerHTML = sth
  }
  const app = new Proxy(data, {
    get() {
      console.log('값 접근')
    },

    set(target, prop, newValue) {
      target[prop] = newValue
      render(newValue)
      console.log('값 갱신')
    }
  })
</script>
<!-- 데이터가 변하는 것에 따라 객체의 내용이 변함에 따라 자연스럽게 화면의 내용도 일치해서 바뀌는 시스템이
바로 리액티비티 시스템임-->
```

- data라는 객체를 만들고 key값은 message에 value값은 10을 설정합니다.
- `render ()`
  - 메세지의 값이 변했을 때 이 콘솔로그만 출력하는 것이 아니라 화면에 출력해보기 위해 위쪽 div 태그에 값이 출력되도록 간단하게 함수를 만들어보겠습니다.
  - `document.querySelector('#app')` 이 코드를 통해 자연스럽게 div 태그로 접근할 수 있는 다큐멘트 쿼리 셀렉터라고 하는 DOM API 입니다.
  - `DOM API` : HTML 태그 정보에 접근할 수 있는 기능입니다.
  - 이렇게 만든 render 함수를 app 객체에 Proxy를 적용할 때 함께 넘겨줍니다.
  - 쿼리 셀렉터의 결과는 div라고 하겠습니다.
  - render()에 값을 넣게 되면 div태그 안쪽에 결과값이 출력됩니다.
- `set()`
  - set에 처음으로 들어오는 값은 target, prop, value 이며 API스펙에 정의되어 있습니다.
  - 객체의 속성 값에다가 새로운 값 value를 넣어줍니다.
  - 단순히 세팅하는 것 뿐만 아니라 render()에 새로운 값을 넣어주면 새롭게 세팅된 값을 속성에 집어넣습니다.
  - 그 다음에 렌더라는 함수를 이용하여 화면에 div 태그에다가 집어넣겠다고 보면 됩니다.

⇒ 데이터가 변하는 것에 따라 객체의 내용이 변함에 따라 자연스럽게 화면의 내용도 일치해서 바뀌는 시스템이 바로 `리액티비티 시스템`입니다.

</details>

<details>
<summary># Vue.js 기본 개념과 문법</summary>
## 앱 인스턴스

Vue로 개발을 시작할 때 기본적으로 생성해야 되는 애플리케이션 인스턴스를 알아보겠습니다.

```jsx
//공식 문서
import { createApp } from 'vue'
const app = createApp({
  /*최상위 컴포넌트 옵션 */
})
```

그 전에 위에서 작성한 코드들을 보겠습니다.

```jsx
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<body>
  <div id="app">{{message}}</div>
</body>

<script>
  Vue.createApp({

    data() {
      return {
        message: 'Hello Vue 3!'
      }
    }
  }).mount('#app')
</script>


```

- `Vue.createApp` 은 애플리케이션 인스턴스를 생성하는 부분입니다.
- Vue는 이렇게 인스턴스를 만들어서 유효하게 다룰 수 있는 화면의 영역을 지정해줘야합니다.
  - 화면의 영역 :`<body>`태그 안에 있는 모든 HTML태그를 의미합니다.
- `.mount(’#app’)` : 어느 부분에다가 vue의 인스턴스를 적용할지 하는 부분이 마운트라고 보면 됩니다.
- 콘솔로 보면 인스턴스를 만들었기 때문에 <Root>를 볼 수 있고 그 안에 데이터까지 볼 수 있습니다.
</details>
