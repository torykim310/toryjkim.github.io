---
title: basic
date: 2021-08-23 00:08:67
category: graphQL
thumbnail: { thumbnailSrc }
draft: false
---

## Before Jump in to GraphQL!!

rest를 잘 사용하다가 왜 GraphQL 이라는 새로운 방식의 데이터 요청 방법이
개발되었을까?

rest는 endpoint를 데이터의 자원의 주소와 맵핑하는 매우 간편한 방식을 사용한다.

하지만 endpoint를 통해 요받은 데이터는 항상 고정된 리소스 형태를 응답받기 때문에 때로는 불필요한 리소스도 포함된다.

예를들어 아래와 같이 `get http://localhost:3000/people/judy` 이 주소를 통해 데이터를 요청하면 id, name, bestFriend, age를 모두 응받받게 된다. 하지만 때로는 age가 필요없는 경우도 있는데, 이렇게 필요한 데이터보다 더 많은 데이터를 응답받는 현상을 Over-Fetching 이라고 한다. 반대로 필요한 데이터보다 적게 응답받아, 여러번 요청해야 하는 경우는 Under-Fetching이라고 하며, 이런한 현상이 네트워크 자원을 낭비하는 일이기 때문에, graphQL은 대표적으로 이 두 가지 문제점을 해결하고자 세상에 등장한 것이다!!

```json
// get http://localhost:3000/people/judy
{
  "id": 1,
  "name": "Judy",
  "bestFriend": "YeongJong",
  "age": "30"
}
```

## Chapter 1. query

graphQL에서 query는 rest의 get과 같은 역할을 한다.

friends에서 id, name, bestFriend만 받아오고 싶을 때 아래와 같이 필요한 field명을 기입하여 선택적으로 정보를 취득할 수 있다.

### 1.1. 필요한 정보만 선택적으로 받아오기

##### 요청 쿼리

```js
query {
  people {
    id
    name
    bestFriend
  }
}
```

##### 결과

```json
{
  "data": {
    "people": [
      {
        "id": "1",
        "name": "Judy",
        "bestFriend": ["YeongJong"]
      },
      {
        "id": "2",
        "name": "HyeonJung",
        "bestFriend": ["Da Eun", "Yurim"]
      }
    ]
  }
}
```

### 이점

- Over-Fetching 문제를 해결하여 데이터 전송량 최적화

### 1.2. 여러 계층의 정보를 한번에 받아오기

##### 요청 쿼리

```js
query {
  people {
    id
    name
    bestFriend
  }
  teams {
    id
    memeber
  }
}
```

##### 결과

```json
{
  "data": {
    "people": [
      ...
    ],
    "memeber": [
      ...
    ]
  }
}
```

### 이점

- Under-Fetching 문제를 해결하며 요청 횟수 최적화

## Chapter 2. mutation

mutation은 rest의 post와 같은 역할을 한다.
단, rest에서는 post, put, delete등의 역할이 쓰임에 따라 나뉘지만
graphQL에서는 apollo와 같은 graphQL 백엔드 서버에서 작성한 쿼리문을 mutation의 내부에서 사용하여 post, put, petch, delete 등의 기능을 수행할 수 있다.

### 2.1. 추가

##### 요청 쿼리

```js
mutation {
  people (input: {
    name: "DuYeong",
    bestFriend: ["JungWon"]
  },) {
    name
    bestFriend
  }
}
```

### 2.2 수정

```js
mutation {
  editTeam(id: 2, input: {
    name: "HyeonJung",
    bestFriend: ["Da Eun"]
  }) {
    name,
    bestFriend,
  }
}
```

### 특징

- 하나의 url(endpoint)로 모든 요청을 처리할 수 있다. 단, 서비스에 따라 장점이 될 수도 단점이 될 수도 있기 때문에 서비스에 알맞은 방식을 채택하는 것이 중요하다.
