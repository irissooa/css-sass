# CSS

> [CSS Reference공식문서](https://developer.mozilla.org/ko/docs/Web/CSS/Reference)
>
> [CSS게임](https://flukeout.github.io/)
>
> [실습](http://jsbin.com/?html,output)
>
> [color tool](https://material.io/resources/color/#!/?view.left=0&view.right=0)
>
> [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
>
> [Flexbox게임 froggy](https://flexboxfroggy.com/#ko)

[toc]

## 1. 의미, 정의

> CSS(Cascading Style Sheet)

### 우선순위 !important > Author Style > User Style > Browser

>`!important` 가능하면 안쓰는게 좋음



## 2. 선택자

- `*` 모두 고름
- tag : `div`.. etc
- id : `#`
- class : `.classname`
- state : `:`
- Attribute : `[]`



## 3. 스타일링

### (참고) 예시

- `^`는 시작하는 단어 `$`는 끝나는 단어

```css
a[href^='naver'] {
    color:purple;
}

a[href$='.com'] {
    color:red;
}
```





## 4. display vs position

> display
>
> `inline` : item
>
> `inline-block` : 박스가 한 줄에 들어갈 수 있을만큼 들어감
>
> `block` : 한줄에 박스하나
>
> postion은 기본값으로 `static` 
>
> `static`은 html에 정의된 순서대로 브라우저 상에 자연스럽게 보여짐
>
> `relative`는 내가 원래 있어야 되는 자리에서 상대적으로 위치가 이동되고
>
> `absolute`는 item이 담겨있는 박스에서 지정한 css만큼 위치가 이동됨(절대적)
>
> `fixed`는 내가 담겨져있는 상자에서 벗어나 `window`안에서 움직임
>
> `sticky` 원래 있어야되는 자리에 있지만 scroll되면 없어지지 않고 원래 있어야 될 자리에 붙어있음



## 5. Flex Box

> 박스와 아이템을 행 또는 열로 자유자재로 배치시킴
>
> `float` 이미지와 텍스트를 어떻게 배치할건지 정의함
>
> `float : left` 이미지가 왼쪽, 텍스트가 이미지를 감싸면서 오른쪽에 위치함
>
> `float:center`, `float:right`가 있음

### 1) container

> container를 꾸밀 속성 값
>
> - display
> - flex-direction
> - flex-wrap
> - flex-flow
> - justify-content
> - align-items
> - align-content

```css
.container {
    /*container에 너는 이제 flexbox라는걸 알려줌*/
    display:flex;
    /*
    중심축 x(수평)
    기본값은 row 왼쪽에서 오른쪽으로 가는 방향
    row-reverse 오른쪽에서 왼쪽으로 가는 방향
    중심축 y(수직)
    column 위에서 아래로
    column-reverse 아래에서 위로
    */
    flex-direction : row;
    /*
    기본값은 nowrap 아이템이 많아져도 한줄에 붙어있음
    wrap 아이템이 한줄에 꽉차면 자동적으로 아래로 내려감
    wrap-reverse 아래에서 위로 올라감
    
    */
    flex-wrap:wrap;
   /*
    flex-flow: column nowrap
    flex-direction + flex-wrap을 한번에 적을 수 있음
    */
    
    /*item을 어떻게 배치할건지*/
    /*
    justify-content : main axis에서 어떻게 배치할지
    flex-start : 기본값 왼쪽에서 오른쪽으로(중심축 : 수평) 위에서 아래로(중심축 : 수직)
    flex-end : 순서는 유지하되 컨테이너 위치가 오른쪽에서 왼쪽(중심축 : 수평) 아래에서 위로지만 flex-direction이 column이면 순서는 유지되기 때문에 제일아래는 10번(중심축 : 수직)
    flex-direction이 column-reverse라면 아래가 1번으로 아래에서 위로 순서가 커짐!
    center : 중간
    space-around:item사이 간격이 같음 하지만 처음과 끝의 바깥쪽은 간격이 같지 않음
    space-evenly:item사이와 처음과 끝의 바깥쪽까지 모두 간격이 같음
    space-between:처음과 끝을 화면에 맞게 배치하고 item사이 간격이 같음
    */
    justify-content:flex-start;
    /*
    align-items 속성은 justify-content 가 주 축을 따라하는 것처럼 교차 축을 따라 플렉스 컨테이너 내부의 항목을 정렬
    baseline :div말고 item의 text의 baseline이 직선이되게 배치
    */
    align-items :baseline;
    /*
    align-content 는 여러 줄의 유연한 상자를위한 것, 항목이 한 줄에있는 경우에는 효과가 없다.(wrap)
    
    */
    align-content:space-between;
}
```



### 2) item

> item을 꾸밀 속성 값
>
> - order
> - flex-grow
> - flex-shrink
> - flex
> - align-self

- `.container`에 `display:flex`가 지정돼있어야됨

```css
.item1 {
    /* order 순서에 맞게 위치 바꿈 -> 근데 잘안쓰임 */
    order:1;
    /*
    컨테이너가 늘어날때 몇배로 늘어나냐
    기본값은 0 -> 그대로
    1 -> 모든 items들한테 이렇게 지정하면 1:1:1..의 비율로 컨테이너 크기가 커지든 작아지든 반영이됨
    어느것 하나만 다른숫자로 한다면 그 비율에 맞춰짐
    */
    flex-grow:1;
    /*
    컨테이너가 작아졌을때 몇배로 줄어드냐
    기본값 : 0
   	이건 전부 1로 하고 만약 하나만 2로 했을때는 컨테이너가 작아질때 2배로 더 작아짐
    */
    flex-shrink:1;
    /*
    item들이 공간을 얼마나 차지하게하는지 세부적으로 지정해줌
    grow나 shrink를 쓰지않고 커질때도 작아질때도 일정한 크기를 지정할 수 있음
    auto가 기본값
    item 각각 60%, 30%, 10% 지정하면 커지든 작아지든 이 비율 유지
    */
    flex-basis:auto;
    /*
    flex: grow, shirnk, basis 한번에 지정
    flex: 2 2 auto
    */
    /*item별로 정렬을 할 수 있음, 컨테이너에 지정된것을 떠나 아이템 하나씩 따로 지정해 줄 수 있음*/
    align-self : center;
    
}
```





### 3) axis

> main axis : flexbox 중심축
>
> cross axis : 중심축과 수직인 축
>
> 중심축을 수평, 수직에 두는것에 따라 cross axis가 달라짐



### (참고)

> `div.container>div.item.item${$}*10` 적고 `tab`하면 아래 코드 자동 생성
>
> `$`는 번호를 순서대로 입력하겠단 뜻

```html
<div class="container">
  <div class="item item1">1</div>
  <div class="item item2">2</div>
  <div class="item item3">3</div>
  <div class="item item4">4</div>
  <div class="item item5">5</div>
  <div class="item item6">6</div>
  <div class="item item7">7</div>
  <div class="item item8">8</div>
  <div class="item item9">9</div>
  <div class="item item10">10</div>
</div>
```

## box-sizing

> [CSS Box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing -->
    <style>
      .box {
        width: 100px;
        height: 100px;
        background-color: red;
      }
      .inner {
        width: 100%;
        height: 100%;
        background-color: blue;
      }
      .box2 {
        padding: 20px;
        /* content-box의 size, padding과 margin을 넣어도 contnet의 크기는 변하지않음 */
        box-sizing: content-box;
        border: 10px solid black;
      }
      .box3 {
        padding: 20px;
        /* border포함한 box의 size, padding과 margin을 넣으면 content의 크기가 변함 */
        box-sizing: border-box;
        border: 10px solid black;
      }
    </style>
  </head>
  <body>
    <h3>Box without padding</h3>
    <div class="box box1">
      <div class="inner"></div>
    </div>

    <h3>Box with padding</h3>
    <div class="box box2">
      <div class="inner"></div>
    </div>

    <h3>Box with padding, boder-box</h3>
    <div class="box box3">
      <div class="inner"></div>
    </div>
  </body>
</html>

```

## Position

### absolute ve relative

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/position -->
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_Block -->
    <style>
      .outer {
        width: 200px;
        height: 200px;
        margin-bottom: 20px;
        background-color: green;
      }
      .box {
        width: 100px;
        height: 100px;
        background-color: red;
        position: relative;
      }
      .inner {
        width: 100%;
        height: 50%;
      }
      .inner1 {
        background-color: blue;
      }
      .inner2 {
        background-color: yellow;
      }

      .box1 .inner1 {
        /* 원래있던 자리를 유지하면서 내가 지정한 위치만큼 상대적으로 이동함 */
        position: relative;
        top: 30px;
        left: 100px;
      }

      .box2 .inner1 {
        /* 원래있던 자리에서 쏙 빠져나와 주변에 같이있던 박스들도 재배치 됨, absolute는 근접한 부모중 static이 아닌 부모의 기준에서 움직임 inner1의 부모중 static(default값)이 아닌게 없다면 body에 맞춤  */
        position: absolute;
        top: 30px;
        left: 100px;
      }
    </style>
  </head>
  <body>
    <div class="outer">
      <div class="box box1">
        <div class="inner inner1">inner1</div>
        <div class="inner inner2">inner2</div>
      </div>
    </div>
    <div class="outer">
      <div class="box box2">
        <div class="inner inner1">inner1</div>
        <div class="inner inner2">inner2</div>
      </div>
    </div>
  </body>
</html>

```

### sticky vs fixed

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/position-->
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_Block -->
    <style>
      .container {
        position: relative;
        top: 100px;
        left: 100px;
        background-color: beige;
      }

      .box {
        width: 80px;
        height: 80px;
        margin-bottom: 20px;
        background-color: chocolate;
      }

      .box2 {
        background-color: hotpink;
        /* 기존의 자리를 유지하다가 스크롤됐을떄 자기 위치를 그대로 유지하고있고, 공간도 그대로 유지하고있다 그래서 다른 요소들도 그 자리에 그대로 있다 */
        /* sticky는 top과 left,를 지정해줘야됨 */
        position: sticky;
        top: 20px;
        left: 20px;
      }

      .box3 {
        background-color: blue;
        /* 들어있는 부모와 상관없이 뷰포트 안에서 포지션이 일어나기 때문에 문서에서 빠져나와 0,0이 지정되는걸 볼 수 있다 */
        position: fixed;
        top: 20px;
        left: 20px;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="box box1"></div>
      <div class="box box2"></div>
      <div class="box box3"></div>
      <div class="box box4"></div>
      <div class="box box5"></div>
      <div class="box box6"></div>
      <div class="box box7"></div>
      <div class="box box8"></div>
      <div class="box box9"></div>
      <div class="box box10"></div>
    </div>
  </body>
</html>

```

## alignment

> **text-align에 대한 추가 설명:**
>
> text-align은 블럭요소 안에서 그안의 컨텐츠들(텍스트 뿐만 아니라 버튼과 같은 인라인요소) 들을 정렬할때 쓸 수 있어요.
>
> **margin에 대해서** 더 공부해 보고 싶으시다면 MDN 사이트에서 [CSS Margin](https://developer.mozilla.org/en-US/docs/Web/CSS/margin)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      .box {
        width: 200px;
        height: 100px;
        background-color: beige;
      }

      .inner {
        width: 50%;
        height: 50%;
        background-color: blue;
      }

      .inner1 {
        /* margin은 수평으로만 중간 정렬이 가능, 수직은 적용이 안됨 */
        margin: auto;
      }

      .box2 {
        /* text가 아니더라도 다른 요소들을 중간정렬할 수 있지만, div는 한줄에 하나씩만 나오도록 돼있기 때문에 변하지 않음 display가 block이 아닌 것들은 중간 정렬이 적용됨 */
        text-align: center;
      }

      .inner3 {
        /* 움직임, rotation이 가능, x축,y축 50%이동 */
        transform: translate(50%, 50%);
      }

      .box4 h1 {
        text-align: center;
        /* 흔하게 쓰는 방법, 폰트높이를 박스높이만큼 인위적으로 줘서 중간으로옴 */
        /* 한줄의 글이라면 해키한 방법으로 이렇게 쓰기도 함 */
        line-height: 100px;
      }
    </style>
  </head>
  <body>
    <h3>margin: auto</h3>
    <div class="box box1">
      <div class="inner inner1"></div>
    </div>
    <h3>text-align: center</h3>
    <div class="box box2">
      <button>Text</button>
    </div>
    <h3>translate(50%, 50%)</h3>
    <div class="box box3">
      <div class="inner inner3"></div>
    </div>
    <h3>Text centering</h3>
    <div class="box box4">
      <h1>Text<br />Text</h1>
    </div>
  </body>
</html>

```



## Background

> [CSS Background](https://developer.mozilla.org/en-US/docs/Web/CSS/background)
>
> [CSS Background image](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/background -->
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/background-image -->
    <style>
      .box {
        width: 100%;
        height: 200px;
        margin-bottom: 20px;
      }

      .box1 {
        background-image: url('https://media.swncdn.com/cms/BST/67912-gettyimages-817147678-kieferpix.1200w.tn.webp');
        /* 반복하지 않기 */
        background-repeat: no-repeat;
        /* 중간이미지가 나옴 */
        background-position: center;
        /* 남은 공간여백을 차지하면서 나옴 */
        background-size: cover;
      }

      .box2 {
        /* 속성값 위치/size 반복 을 한줄로 적을 수 있음 */
        background: center/cover no-repeat
          url('https://media.swncdn.com/cms/BST/67912-gettyimages-817147678-kieferpix.1200w.tn.webp');
      }

      .box3 {
        background: repeat left
          url('https://media.swncdn.com/cms/BST/67912-gettyimages-817147678-kieferpix.1200w.tn.webp');
      }
    </style>
  </head>
  <body>
    <div class="box box1"></div>
    <div class="box box2"></div>
    <div class="box box3"></div>
  </body>
</html>

```



## transform

> [CSS Transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/transform -->
    <style>
      .box {
        width: 100px;
        height: 120px;
        background-color: brown;
        margin-bottom: 20px;
      }
      /* X축은 오른쪽으로 갈수록 커지고 */
      /* Y축은 아래로 내려갈수록 커짐 */
      .box1 {
        /* X축에서 100px이동 */
        transform: translateX(100px);
      }

      .box2 {
        /* X축, Y축 이동 */
        transform: translate(-50px, -20px);
      }

      .box3 {
        /* 커짐 1.2배 */
        transform: scale(1.2);
      }

      .box4 {
        /* 돌림 */
        transform: rotate(45deg);
      }

      .box5 {
        /* 한번에 옮기고, 애니메이션도 줄수있음 */
        transform: translate(100px, 100px) scale(2) rotate(46deg);
      }
    </style>
  </head>
  <body>
    <div class="box box1"></div>
    <div class="box box2"></div>
    <div class="box box3"></div>
    <div class="box box4"></div>
    <div class="box box5"></div>
  </body>
</html>

```



## transition

> [CSS Transition](https://developer.mozilla.org/en-US/docs/Web/CSS/transition)
>
> [Animation timing function](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function)
>
> [Cubic bezier](https://cubic-bezier.com/)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/transition -->
    <!-- https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function -->
    <!-- https://cubic-bezier.com/ -->
    <style>
      .box {
        width: 100px;
        height: 100px;
        margin: 20px;
        background-color: pink;
      }

      .box1:hover {
        background-color: blueviolet;
        /* 배경색을 0.3초동안, 일정한속도로 */
        transition: background-color 300ms linear;
      }

      .box2:hover {
        border-radius: 50%;
        background-color: cornflowerblue;
        /* 위속성 전부, 2초동안 천천히 */
        transition: all 2s ease;
      }

      .box3:hover {
        border-radius: 50%;
        transform: translateX(400px);
        background-color: cornflowerblue;
        transition: all 3s ease;
      }
    </style>
  </head>
  <body>
    <div class="box box1"></div>
    <div class="box box2"></div>
    <div class="box box3"></div>
  </body>
</html>

```



## CSS variables

> https://developer.mozilla.org/en-US/docs/Web/CSS/--*