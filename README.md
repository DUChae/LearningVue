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
