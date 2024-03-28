# 클로저란 무엇인가 설명해주세요.

클로져는 어떤 함수(outer) 내부에 선언된 함수(inner)가 바깥 함수(outer)의 지역변수(outerVariable)를 참조하는 것이 함수(outer)가 종료된 이후에도 계속 유지되는 현상을 말한다.

```jsx
const outer = () => {
  const outerVariable = 'outer!'; // 1. 바깥 함수 outer의 스코프에 변수선언

  const inner = () => {
    console.log(outerVariable); // 2. 내부 함수 inner의 스코프에서 스코프체인을 타고 바깥 함수 스코프의 변수 참조
  };

  return inner; // 3. 1급 시민인 함수 inner를 바깥으로 반환
};

const newFunc = outer(); // 4.  newFunc에 inner함수의 주소값이 저장됨

newFunc(); // 5. outer함수 호출은 종료가 되어서 스코프가 사라져야 하지만 outerVariable은 여전히 잘 참조된다.
```

## 실행 컨텍스트

**실행할 코드에 제공할 환경 정보들을 모아놓은 객체**

실행 컨텍스트 내부엔 **`variable environment`**, **`lexical environment`**, **`this binding`** 가 있다.

VariableEnvironment 란 현재 컨텍스트 내부의 식별자 정보 **`environmentRecord`**, 외부 환경 정보 **`outerEnvironmentReference`**가 포함

LexicalEnvironment 는 초기에는 VariableEnvironment 와 같지만 변경 사항이 실시간으로 적용된다.

즉, VariableEnvironment **초기 상태를 기억**하고 있으며, LexicalEnvironment **최신 상태를 저장**하고 있다.

## 스코프

변수에 접근할 수 있는 범위

자바스크립트는 함수를 선언할 때마다 새로운 스코프를 생성한다. 함수 안에서 선언한 변수는 해당 함수 안에서만 접근할 수 있는데 이걸 함수 스코프라고 한다.

### 스코프 체인

Identifier를 찾는 일련의 과정

찾을 때 까지 계속적으로 감싸고 있는 상위 함수를 탐색하는 과정을 거친다.

> 주의: 바로 바깥 스코프는 함수를 실행하는 시점의 바깥영역이 아닌 선언되는 시점의 바깥 스코프를 가리킨다는 것! ( = 렉시컬 스코프)
> 
> https://ljtaek2.tistory.com/145
> 

## 참조
[클로져와 가까워지기](https://tecoble.techcourse.co.kr/post/2021-07-16-closure/)

[클로져(Closure)는 무엇이며, 어떻게/왜 사용하는가?](https://born-dev.tistory.com/30)