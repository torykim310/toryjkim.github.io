---
title: typescript-react
date: 2021-08-12 20:08:13
category: typescript
thumbnail: { thumbnailSrc }
draft: false
---

## TypeScript

TypeScript에 대해 알아보자!

TypeScript는 공식 페이지에서 javascript의 superset이라고 소개한다. [공식문서](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-1.html#support-for---target-es2016---target-es2017-and---target-esnext)에 따르면 TypeScript 2.1 부터 --target ESNext를 지원하니, 웬만한 js 문법은 전부 사용할 수 있고 컴파일을 통해 타입체크도 할 수 있으니 superset이라고 부를 수 있겠다.

## React와 함께 사용하기

### 1. 함수 컴포넌트 prop 타입 지정하기

컴포넌트의 prop 타입을 지정하는 방법은 크게 2가지가 있다.

#### 1.1. React.FC 와 제네릭

```js
import React from 'react';

interface GreetingProps {
  name: string;
  mark: string;
}

const Greeting: React.FC<GreetingProps> = ({ name, mark, optional }) => {
  return (
    <div>
      Hello {name} {mark}
    </div>
  );
};

Greeting.defaultProps = {
  mark: '!',
};

const App = () => {
  return (
    <Greeting name="YeongJong" /> // Property 'mark' is missing in type
  );
};
```

const로 선언한 함수에서 **React.FC\<GreetingProps>** 와 같이 제네릭 방식으로 타입을 설정할 수 있다.

##### 특징

1. children의 propType이 React.ReactNode 기본 설정되어 있기 때문에 children의 propType 설정이 필요하지 않다.
2. defaultProp이 제대로 적용되지 않는다. (위 예시의 경우 mark는 '!'로 기본 설정되었지만, Greeting을 호출할 때 mark prop을 넘겨주지 않으면 에러 발생)

> 2번 참고자료: https://github.com/typescript-cheatsheets/react/issues/87

#### 1.2 function 키워드로 선언한 함수의 type으로 적용

```js
import React from 'react';

interface GreetingProps {
  name: string;
  mark: string;
}

function Greeting({ name, mark, optional }:GreetingProps) => {
  return (
    <div>
      Hello {name} {mark}
    </div>
  );
};

Greeting.defaultProps = {
  mark: '!',
};
```

##### 특징:

1. children의 propType이 기본 설정되어 있지 않다. 따라서 children을 삽입할 경우에 propType 설정이 필요하다.
2. defaultProps가 제대로 적용된다.

#### 1.3 소결론

React.FC는 defaultProps가 적용되지 않는 문제점 그리고, children이 기본 적용되어 있기 때문에 children이 삽입되지 않는 경우에 문제가 발생할 수 있다. 따라서 function 키워드를 통한 type 설정을 권장한다.

##### reference

- [React + TypeScript CheatSheets](https://github.com/typescript-cheatsheets/react#reacttypescript-cheatsheets)
