# 싱글스레드 언어인 자바스크립트가 비동기처리가 될 수 있는 그 배경을 설명해주세요.
자바스크립트의 V8엔진은 싱글 스레드를 가지고 있어서, 단 하나의 Call Stack을 가지고 있다. 따라서 동기적으로 실행되어야 하는데, 어떻게 비동기적으로 실행될 수 있을까?

자바스크립트 엔진 말고도 Web API, Task Queue, Event loop이 자바스크립트 실행에 관여한다.

## 이벤트 루프

이벤트 루프는 브라우저 내부의 Call Stack, Callback Queue, Web APIs 등의 요소들을 모니터링하면서 비동기적으로 실행되는 작업들을 관리하고, 이를 순서대로 처리하여 프로그램의 실행 흐름을 제어한다.

자바스크립트의 setTimeout이나 fetch같은 비동기 작업을 브라우저의 Web APIs에게 맡기고,  백그라운드 작업이 끝나면 Callback Queue에 넣는다. 그리고 처리가 준비되면,  Call Stack에 넣어 마무리 작업을 하게 된다.

이벤트 루프는 Call Stack에 현재 실행 중인 작업이 있는지 그리고 Task Queue에 대기 중인 작업이 있는지 반복적으로 확인하는 일종의 무한 루프만을 돌고, 대기 작업이 있다면 작업을 옮겨주는 형태로 동작한다.

> **NodeJS 환경**도 브라우저와 거의 비슷하다
> 
> 
> Web API가 아닌 Node.js API를 사용하여 파일 시스템 액세스, 네트워크 액세스, 암호화, 압축 및 해제 등과 같은 다양한 작업을 처리한다.
> Event Queue: Task Queue와 비슷
> 
> `libuv`라는 라이브러리를 사용하고, 이 라이브러리에서 이벤트 루프를 제공하는 형태
> 

> 웹브라우저의 Web APIs는 비동기 작업이 끝나면 스스로 callback queue에 적재하지만, Node.js API들은 이벤트 루프가 직접 옮겨준다.
> 

## Web APIs

타이머, 네트워크 요청, 파일 입출력, 이벤트 처리 등 브라우저에서 제공하는 다양한 API를 포괄하는 총칭이다. 브라우저에서 멀티 쓰레드로 구현되어 있기 때문에 비동기 작업이 가능하다. (동기적으로 실행되는 Web API도 있다 - DOM API, Console API)

## Callback Queue

### Task Queue

setTimeout, setInterval, fetch, addEventListener와 같이 비동기 함수들의 콜백함수가 들어가는 큐

### Microtask Queue

promise.then, promise.nextTick, MutationObserver와 같이 우선순위가 높은 비동기 함수들의 콜백함수가 들어가는 큐

> 먼저 microtask queue를 처리하여 먼저 비우고 그다음 task queue의 콜백을 처리한다. 그렇기 때문에 promise.then 결과가 setTimeout보다 먼저 처리된다!
> 

### AnimationFrame Queue

`requestAnimationFrame` 메서드를 통해 콜백을 등록하면, 이 큐에 적재되어 브라우저가 repaint 직접에 큐에 있는 모든 작업을 처리한다

## 참조
[🔄 자바스크립트 이벤트 루프 동작 구조 & 원리 끝판왕](https://inpa.tistory.com/entry/🔄-자바스크립트-이벤트-루프-구조-동작-원리)