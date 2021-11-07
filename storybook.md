# Storybook.js

**리엑트를 기준으로 Storybook 환경을 설정합니다.**

StoryBook.js 는 컴포넌트를 자동으로 문서화하며 시각적으로 테스트할 수 있게 도와주는 도구다. 기존 TDD 방식과 다르게 CDD 즉 컴포넌트 단위로 작성하고 테스트한다는 특징을 가지고 있다.

## What's a story?

Storybook에서는 하나의 story가 특정 상태의 컴포넌트를 캡처한다고 설명하고 있습니다. 이 말이 무슨 의미인지 나름대로 해석해 봤습니다.(개인적인 견해임을 참고해주세요!)

하나의 컴포넌트는 state 혹은 prop에 따라 렌더링 결과물이 달라집니다. storybook을 작성하는 형태도 아래 예시와 같이 컴포넌트의 state 혹은 prop에 따라 구분하여 작성하는데요.
Button 컴포넌트는 prop에 따라 Primary, Secondary, Large, Small이라는 이름이 부여됐고 각각은 하나의 스토리라고 볼 수 있습니다. 마치 버튼이라는 주인공이 상황에 따라 Primary, Secondary, Large, Small 이라는 이야기를 그려 간다고 생각하면 될 것 같아요.

버튼 스토리 외에도 링크헤더 등 다양한 주인공을 설정하고 스토리를 작성할 수 있고 이 단편 스토리들이 모여 하나의 장편 스토리들을 만들겠죠. 완성된 장편 스토리는 컴포넌트 관점에서 보면 Page에 해당할 것 입니다.

## 오늘의 예제

```js
import React from 'react';

import { Button } from './Button';

export default {
  title: 'Example/Button',
  component: Button,
  argTypes: {
    backgroundColor: { control: 'color' },
  },
};

const Template = args => <Button {...args} />;

export const Primary = Template.bind({});
Primary.args = {
  primary: true,
  label: 'Button',
};

export const Secondary = Template.bind({});
Secondary.args = {
  label: 'Button',
};

export const Large = Template.bind({});
Large.args = {
  size: 'large',
  label: 'Button',
};

export const Small = Template.bind({});
Small.args = {
  size: 'small',
  label: 'Button',
};
```

## 설명

1. Component.stories.js 파일을 만들고 meta 정보를 default로 export 하기

```js
import React from 'react';

import { Button } from './Button';

// 해당 컴포넌트의 메타정보를 export default 합니다.
export default {
  title: 'Components/Button', // 단편 스토리 제목 지정
  component: Button, // 스토리의 주인공 컴포넌트 지정
};
```

2. 주인공의 이야기 생성

```js
...
const Template = args => <Button {...args} />;

// Primary, Secondary, Large, Small은 Button의 특정 스토리(이야기)에 해당
export const Primary = Template.bind({});
Primary.args = {
  primary: true,
  label: 'Button',
};

export const Secondary = Template.bind({});
Secondary.args = {
  label: 'Button',
};

export const Large = Template.bind({});
Large.args = {
  size: 'large',
  label: 'Button',
};

export const Small = Template.bind({});
Small.args = {
  size: 'small',
  label: 'Button',
};
```

## 트러블 슈팅

storybook을 매뉴얼로 구성하는 경우, webpack에 의존하기 때문에 webpack을 올바르게 설정해야 합니다. storybook에서는 postcss가 deprecated되었으며 @postcss를 설정하다 `get of undefined` 에러가 발생한다면, storybook init 시 builder 설정이 webpack4(default)로 설정되어 있어 버전 문제가 발생했을
