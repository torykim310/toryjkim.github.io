---
title: media query
date: 2021-04-27 01:04:51
category: css
thumbnail: { thumbnailSrc }
draft: false
---

# media-query

미디어 쿼리는 미디어 유형과, 미디어의 특성에 따라 스타일을 지정하고 싶을 때 사용한다.

## 1. 문법

```
@media 조건 {
    css 문법
}
```

> 참고1
> 조건에는 미디어의 유형 또는 특성을 입력한다.

> 참고2
> 조건을 충족하면 {} 내에 작성한 css 문법이 적용된다.

### 1.1 논리 연산자

`not`, `and`, `or`, `only`와 같은 논리 연산자를 사용해서 쿼리를 조합하면 복잡한 조건식을 만들 수 있다.

#### a and b:

`and` 연산자를 사용하면 조건 `a`와 `b`를 모두 충족해야 스타일이 적용된다.

#### a or b:

`or`을 사용하면 다수의 기능을 판별해서 하나라도 맞는 경우 스타일을 적용시킬 수 있습니다.

#### not a and b

`not` 연산자를 사용하면 이따라 작성된 전체 조건식의 의미를 반전시킨다. 즉 a 조건에만 적용되는 것이 아니고 a and b에 적용된다.

> @media not all and (monochrome) {...}
> 위의 쿼리는 아래와 같이 평가된다.
> @media not(all and (monochrome)) {...}
> 아래와 같이 평가되는 것이 아니다.
> @media (not all) and (monochrome) {...}

#### only

`only` 연산자는 전체 쿼리가 일치할 경우에만 스타일이 적용된다.

`screen and (max-width: 500px)` 쿼리를 작성했을 때 구형 브라우저에서 `max-width:500px` 부분을 인식하지 못하기 대문에 screen 조건이 참이되면 스타일을 적용해 버린다. 이와 같은 오류를 방지하기 위해 `only`를 사용할 수 있다.

#### ,(쉼표)

다수의 미디어 쿼리를 한줄에 작성하고 싶을 때 사용합니다.

## 3. 실습

## 4. 장점

## 5. 단점

## 6. 활용방안

max-width, min-width 특성을 조건문으로 설정하면 뷰포트의 너비에 따라 스타일을 다르게 적용하여 반응형 웹을 구현할 수 있습니다.

### 참고자료

- https://developer.mozilla.org/ko/docs/Web/CSS/Media_Queries/Using_media_queries
