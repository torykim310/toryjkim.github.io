---
title: router
date: 2021-09-02 11:08:33
category: react
thumbnail: { thumbnailSrc }
draft: false
---

## 1. Before Jumpo into React Router

ROUTER에 대해 학습하기 전 SSR과 CSR에 대해 간략하게 알고 넘어가자!
SSR과 CSR은 페이지와 관련이 깊다. 페이지의 구조를 담당하는 HTML 파일을 어느 위치에서 생성할 것인지에 따라 SSR과 CSR로 나뉘게 된다.

### 1.1 SSR

SSR은 사용자가 서버에게 페이지 리소스를 요청하면, 서버는 요청에 해당하는 HTML 파일을 생성하여 전송한다.

#### 장점

- HTML 코드를 완성해서 보내기 때문에, 검색 엔진 최적화가 가능함.
- 첫 페이지 렌더링은 일반적으로 CSR보다 빠르다.
  - CSR은 HTML을 생성하는 번들러를 받아온 후 HTML을 생성하는 과정이 필요하기 때문

#### 단점

- 페이지마다 html 파일을 요청하기 때문에 요청 횟수가 증가한다.
- 따라서 첫 페이지 렌러딩 외에는 일반적으로 CSR보다 렌더링 속도가 느리다.

### 1.2. CSR

CSR은 초기에 최소한의 코드를 포함한 HTML을 전송 받은 후, JS 파일을 통해 HTML의 메인 코드들을 동적으로 생성합니다.

#### 장점

- 서버에 요청 수가 줄어듦에 따라 서버의 부담을 덜어 낼 수 있다.
- 두번째 렌더링 부터는 HTML요청 없이 JS를 통해 렌더링하기 때문에 SSR 보다 빠르다.

#### 단점

- 최소한의 코드를 포함한 HTML은 검색 엔진에 전달할 정보가 부족하므로 포털에 SEO 점수가 낮게 평가됩니다.
- 번들된 JS 파일의 크기가 커질 경우 초기 렌더링이 느려지기 때문에 최적화가 필요합니다.

## 2. React Router

클라이언트 사이드에서 라우팅하기 위한 라이브러리로 **react-router-dom**을 사용할 수 있다.

1. Router: Route(경로)들을 관리한다.
2. Route: 특정 경로(path)가 입력되면 component를 렌더링 한다.
3. Switch: 첫번째로 매칭되는 Route만 렌더링 되도록 하는 도구
   > (switch가 없다면 루트 경로로 이동하고자 하는 경우 "/"를 포함한 Route가 모두 렌더링 되는 문제가 발생한다. 아래 예시의 exact를 기입했음에도 dashboard, products, landing이 모두 렌더링 됨.)
4. Redirect

```ts
import {
  BrowserRouter as Router,
  Route,
  Switch,
  Redirect,
} from 'react-router-dom';
import { Landing, Products, Dashboard } from 'pages';
import { Header, Footer } from 'containers';

export default function WireframeApp() {
  return (
    <Router>
      <Switch>
        <Route exact path="/" component={Landing} />
        <Route path="/dashboard" component={Dashboard} />
        <Route path="/products" component={Products} />
        <Redirect to="/landing" />
      </Switch>
    </Router>
  );
}
```

## 3. storybook with router

리엑트의 경우 Link 컴포넌트를 통해 경로를 이동시킬 수 있다.

이 때, Link는 Router 컴포넌트 내에서만 사용할 수 있기 때문에, Link 컴포넌트를 테스트하고 싶은 경우, decorator를 사용하여 Router를 감싸 줄 수 있다.

```ts
export default {
  title: 'Components/Nav',
  component: Nav,
  decorators: [
    Story => (
      <Router>
        <Story />
      </Router>
    ),
  ],
} as ComponentMeta<typeof Nav>;

const Template: ComponentStory<typeof Nav> = args => <Nav {...args} />;

export const Basic = Template.bind({});
```
