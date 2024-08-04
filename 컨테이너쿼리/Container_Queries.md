# CSS Media Query VS Container Queries

## Media Query
 - 유저가 **지정한 규칙에 브라우저 및 장치 환경이 일치하는 경우에만 CSS를 적용**할 수 있는 방법을 제공
 ```css
@media screen and (min-width: 1280px) {
        margin-bottom: 15vh;
} {/* 뷰포트 너비가 1280px 이상일 때 margin-bottom 15vh*/}
 ```

## Container Queries
- 특정한 컨테이너 요소의 크기 변화에 따라 그 요소와 요소 안의 자식 요소들 스타일을 변경 가능
- 각 요소의 크기나 모양에 따라 반응형 쿼리를 지정 가능
![컨테이너의 크기에 따라 배치가 변경되는 예제(1/2)](https://github.com/user-attachments/assets/ec1aedb2-4187-4d75-bb13-69036fb7ac43)
![컨테이너의 크기에 따라 배치가 변경되는 예제(2/2)](https://github.com/user-attachments/assets/40d7da69-7ff1-45ec-83e9-8189b0310ca1)
##### https://www.oddbird.net/2021/04/05/containerqueries/

### 컨테이너 쿼리 사용법
1. container-type
- 반응형 스타일링을 적용할 요소를 감싸고 있는 컨테이너의 선언

(1) Keyword Values
 ```script
 🐈 컨테이너의 크기는 어떤 것을 기준으로 할 것인가?
  ```
- `size` : 가로와 세로의 크기에 모두 반응
- `inline-size` : 가로 크기에 반응
- `block-size` :세로 크기에 반응
 ```css
 .Walrein {
  container-type: inline-size;
}
  ```

(2) Global Values
 ```script
🐈 컨테이너 초기값과 상속에 관련된 것
 ```
- `inherit` : 부모 요소의 속성 값을 상속
- `initial` : 브라우저가 지정한 초기값을 상속
- `revert` : 현재 스타일 시트를 무시하고 부모속성으로 부모가 없을때는 초기속성으로
-`revert-layer` : 현재 레이어의 스타일 대신 이전 레이어의 스타일 적용
- `unset` : 부모속성을 상속. 부모가 없다면 초기속성을 사용
 ```css
 .Walrein {
  container-type: inline-size;
}
  ```

2. container-name
반응형 스타일링을 적용할 요소를 감싸고 있는 컨테이너의 이름 지어주기
 ```css
 .Walrein {
  container-type: inline-size;
  container-name: Sealeo, Spheal;
}
  ```

3. 선언된 컨테이너 사용
 ```css
@container Sealeo (min-width: 700px) {
  .Sealeo {
    font-size: max(1.5em, 1.23em + 2cqi);
  }
}

@container Spheal (min-width: 700px) {
  .Spheal {
    font-size: max(1.5em, 1.23em + 2cqi);
  }
}
 ```

 #### container - container-type과 container-name 한번에 설정하기
 container 속성을 사용하면 `container-type`과 `container-name`을 한번에 설정

  ```css
.Walrein {
  container: Sealeo / inline-size, Spheal / inline-size;
}
 ```

 ### 컨테이너 쿼리의 길이 단위
 -  ##### [Container Length Units : 이미지 자료가 있음] (https://css-tricks.com/css-container-queries/)
 - viewport의 vw , vh 와 같이 container에 상대적인 단위들
 - `cqw`: 쿼리 컨테이너 너비의 1%
 - `cqh`: 쿼리 컨테이너 높이의 1%
 - `cqi`: 쿼리 컨테이너의 인라인 크기의 1%
 - `cqb` : 쿼리 컨테이너 블록 크기의 1%
 - `cqmincqi`: 둘 중 더 작은 값
 - `cqmaxcqi`: 둘 중 더 큰 값

### Media Query < Container Queries
Container Queries를 사용할 때, 전체 문서(루트 요소)를 컨테이너로 지정하면 미디어 쿼리와 유사한 효과를 얻을 수 있음
그러나 Container Queries를 사용하는 것이 더 간결하고 유연성이 높은 경우가 많다
(1) Media Query 예제
```html
<!DOCTYPE html>
<head>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <div class="container-child"></div>
    </div>
</body>
</html>
```
 ```css
.container {
  padding: 20em;
  background-color: red;
}

.container-child {
  padding: 10em;
  background-color: pink;
}

@media (max-width: 767px) {
  .container {
    background-color: blue;
  }

  .container-child {
    background-color: yellow;
  }
}

@media (min-width: 1024px) {
  .container {
    background-color: green;
  }

  .container-child {
    background-color: skyblue;
  }
}
 ```

 (2) Container Queries 예제
   ```html
<!DOCTYPE html>
<head>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <div class="container-child"></div>
    </div>
</body>
</html>
   ```
   ```css
.container {
  container-type: inline-size;
  container-name: ctn1;
  padding: 20em;
  background-color: red; 
}

.container-child {
  padding: 10em;
  background-color: pink; 
}

@container ctn1 (min-width: 1024px) {
  .container {
    background-color: green;
  }

  .container-child {
    background-color: skyblue; 
  }
}

@container ctn1 (max-width: 767px) {
  .container {
    background-color: blue; 
  }

  .container-child {
    background-color: yellow; 
  }
}
   ```
## Media Query and Container Queries의 공통점
- 문서의 스타일을 반응형으로 지정 가능

## 정리
- Media Query 
        - 화면 전체를 기준으로 (ex. 뷰포트의 크기나 사용자가 어떤 기기를 사용하는지) 스타일을 적용함.
        - 각 요소에 스타일을 지정할 수는 없다.
        - 전체 페이지의 레이아웃에 영향을 미침

- Container Queries
        - 컨테이너(요소)단위를 기준으로 스타일을 적용함.
        - 각 요소에 스타일을 지정 가능하다. -> **유연함.**
        - 전체 페이지의 레이아웃에 영향을 미치지 않음. 

## 본인 생각
- Container Queries의 등장으로 보다 사용자 경험을 향상시킬만한 인터렉티브 웹을 제작할 수 있을 것이라고 생각함. <br>
ex. 웹에 맵크기조절 가능한 팝업창을 띄우고 팝업창 안의 요소들을 재 정렬해야 할 때 등 유용할 것 같은 일들이 많다고 생각됨.
- 반응형 웹을 만들때 뷰포트와 관련된 스타일은 미디어쿼리로 적용하고, 컨테이너 쿼리로 디테일을 살려주면 좋을 것 같다고 생각됨.

## 읽어본 자료들
https://www.instagram.com/p/C-K8V33Sh4k/?utm_source=ig_web_copy_link&igsh=MzRlODBiNWFlZA== <br>
https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_containment/Container_queries<br>
https://developer.mozilla.org/en-US/docs/Glossary/Media_query<br>
https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries<br>
https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_containment/Container_size_and_style_queries<br>
https://inpa.tistory.com/entry/%F0%9F%8C%9F-css-container-%EC%82%AC%EC%9A%A9%EB%B2%95<br>
https://developer.mozilla.org/en-US/docs/Web/CSS/container-type<br>
https://mong-blog.tistory.com/entry/CSS-Container-%EC%BF%BC%EB%A6%AC%ED%8A%B9%EC%A0%95-%EC%9A%94%EC%86%8C-%ED%81%AC%EA%B8%B0%EC%97%90-%EB%94%B0%EB%9D%BC-%EC%8A%A4%ED%83%80%EC%9D%BC%EB%A7%81%ED%95%98%EA%B8%B0#google_vignette <br>
https://www.oddbird.net/2021/04/05/containerqueries/<br>
https://alistapart.com/article/container-queries-once-more-unto-the-breach/