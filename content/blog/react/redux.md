# Jump into Redux

Redux는 글로벌 상태 관리 도구다. 기존 useState 통해 지역으로 상태를 관리하면 props drilling에 빠질 수 있어 상태 관리가 힘들어진다.

이에 대응할 수 있는 방법은 아래와 같다.

1. createContext를 사용하여 Provider를 통해 최상위 컴포넌트에서 전역으로 상태를 관리할 수 있다. Consumer 혹은 useState를 사용하면 context가 관리하고 있는 상태를 어디서든 접근할 수 있다.

```js
const testContext = createContext();
```
