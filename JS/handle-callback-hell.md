# 콜백지옥을 해결할 수 있는 방법

콜백 헬이란 여러 콜백 함수가 중첩되어 코드의 가독성과 유지보수성을 떨어트리는 현상을 의미합니다.

```js
const fs = require("fs");

fs.readFile("file1.txt", "utf8", (err, data1) => {
  if (err) {
    console.error("첫 번째 파일 읽기 실패:", err);
    return;
  }
  console.log("첫 번째 파일 읽기 성공:", data1);

  fs.readFile("file2.txt", "utf8", (err, data2) => {
    if (err) {
      console.error("두 번째 파일 읽기 실패:", err);
      return;
    }
    console.log("두 번째 파일 읽기 성공:", data2);

    fs.writeFile("combined.txt", data1 + data2, (err) => {
      if (err) {
        console.error("파일 쓰기 실패:", err);
        return;
      }
      console.log("파일 결합 성공");
    });
  });
});
```

콜백 헬을 해결하기 위해 <b>두가지 방법</b>을 사용할 수 있습니다.

### 1. Promise 객체 사용

Promise ES6에 등장한 비동기 작업을 위한 객체로 중첩된 콜백 대신 연쇄적인 then메서드를 사용해서 비동기코드를 더 가독성 좋게 만들어 줍니다. 여기서 연쇄적인 then 메서드 사용을 promise chaining이라고 합니다.

```js
fs.readFile("file1.txt", "utf8")
  .then((data1) => {
    console.log("첫 번째 파일 읽기 성공:", data1);
    return fs.readFile("file2.txt", "utf8");
  })
  .then((data2) => {
    console.log("두 번째 파일 읽기 성공:", data2);
    return fs.writeFile("combined.txt", data1 + data2);
  })
  .then(() => {
    console.log("파일 결합 성공");
  })
  .catch((err) => {
    console.error("오류 발생:", err);
  });
```

### 2. async/await 사용

ES2017에 등장한 키워드로 비동기 코드를 동기 코드로 보이게 하여 가독성을 향상시킵니다. async 함수 안에 await 키워드를 사용해서 프라미스가 완료될 때 까지 함수의 동작을 일시적으로 멈추게 할 수 있습니다.

```js
async function readFile() {
  try {
    const data1 = await fs.readFile("file1.txt", "utf8");
    const data2 = await fs.readFile("file2.txt", "utf8");
    await fs.writeFile("combined.txt", data1 + data2);
  } catch (error) {
    console.error(error);
  }
}
```
