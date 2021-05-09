---
title: scss
date: 2021-05-01 00:05:95
category: css
thumbnail: { thumbnailSrc }
draft: false
---

# scss

scss는 sass의 3번 버전으로 css 전처리기입니다. css에 왜 전처리기가 필요할까요? css를 접해봤다면 반복되는 작업을 수행할 수 없기 때문에 코드의 길이가 상당히 길어지게 됩니다. 이렇게 긴 css 코드는 구조를 파악하기 힘들어지며 이 것은 생산성과도 직결됩니다. 그 외에도 여러가지 이유가 있지만 scss를 사용하면 선택자를 재사용할 수 있고 전체 구조를 파악하기도 훨씬 쉬워집니다.

## sass 설치

\- window 용
`choco install sass`

window의 cli installer인 choco를 사용해서 간단하게 설치할 수 있습니다.

## --watch option

sass의 --watch option은 특정 파일 혹은 폴더를 실시간으로 추척해서 변화가 감지될 때마다, sass로 작성된 파일을 scss로 컴파일 합니다.
`sass -watch app/sass:public/stylesheets`
