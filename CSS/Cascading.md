# 캐스캐이딩( Cascading )
css의 스타일 우선순위

HTML element는 하나 이상의 스타일에 영향을 받을 수 있기 때문에, 어떤 스타일을 적용 받을지에 대한 우선순위가 결정되어야 합니다.

이를 캐스캐이딩 이라고 하는데, CSS의 정식 명칭은 Cascading Style Sheets인 만큼 캐스캐이딩이 중요하다는 것을 알 수 있습니다.

캐스캐이딩은 다음의 3가지에 의해 결정됩니다.

- CSS가 어디에서 선언되었는지 ( 중요도 )
- 대상을 명확하게 지정할수록 ( 명시도 )
- 코드 순서

<br/>

## 중요도
1순위: 사용자 스타일 시트  
특별한 조건이 필요한 사용자가 그들의 필요에 맞게 구성해 놓은 스타일 시트를 말합니다.  
예를들어 저시력자는 글자를 명확히 읽기 위해 윈도우의 '고대비' 설정 기능을 사용할 수 있습니다. 그러면 그러한 스타일이 시스템에 저장되게 되는데, 그것이 '사용자 스타일 시트'입니다. 사용자 스타일 시트는 사용자가 시스템에 저장한 스타일이기 때문에, 웹페이지 제작자가 스타일을 제어할 수 없습니다.

2순위: 제작자가 만든 !important 스타일   
웹페이지 제작자가 스타일 시트에 스타일을 만들 때 속성값 뒤에 !important라고 써놓은 것을 말합니다.
```
<head>
    <style>
        p {
            color: orange !important;
        }
    </style>
</head>
<body>
    <p style="color:brown">hello</p>
</body>
```

3순위: 제작자가 만든 일반 스타일   
우리가 지금까지 계속 사용해왔던 그러한 일반적인 스타일들을 말합니다.
```
test.css

p {
    color: blue;
}
```

4순위: 기본적인 브라우저 스타일   
브라우저들마다 기본적으로 지정하고 있는 스타일입니다. 즉 크롬, 익스플로러, 파이어폭스 등 웹브라우저들이 기본적으로 지정해놓은 스타일들을 말합니다.

<br/>

## 명시도
1. !important
2. inline 스타일
3. 아이디 selector
4. 클래스 / 가상 선택자
5. 태그 선택자
6. 상속된 스타일

!important는 거의 우선순위 끝판왕이지만, 그렇다고 남용하는 것은 좋지 않습니다.   
inline은 높은 우선순위를 갖지만, inline으로 스타일을 주지 말고, `<style>`이나 외부 CSS 파일로 빼는 것이 좋습니다.

<br/>

## 코드 순서
늦게 선언된 스타일이 우선 적용됩니다.
```
<style>
  p {
    color: red;
  }

  p {
    color:blue;
  }
</style>
<body>
    <div>
        <p>Hello</p>
    </div>
</body>
```
위와 같은 HTML이 있을 때 Hello의 글자 색은 blue입니다.

<br/>

## Specificity Calculator
HTML 요소에 같은 스타일이 적용된다면 캐스캐이딩에 의해 어떤 스타일이 적용될지 결정됩니다.   
그리고 위에서 살펴본 "코드순서"에 따르면 아래의 `<p>` 태그의 글자 색은 어떤 색이 될까요?
```
<style>
  div p {
    color: red;
  }

  p {
    color:blue;
  }
</style>
<body>
    <div>
        <p>Hello</p>
    </div>
</body>
```
코드 순서에 따르면 p가 나중에 적용되었으므로 파란색이 되어야 할 것입니다.   
그러나 결과는 빨간색입니다.


이와 관련된 개념은 Specificity Calculator 입니다.

즉, 어떤 스타일이 적용이 될지 일종의 점수를 매기는 것인데요,  
1번의 경우 `<div> , <p>` 두 요소에 대하여 스타일이 적용되어야 하므로 2점   
2번의 경우에는 `<p>` 요소에 대해서만 스타일이 적용되므로 1점입니다.

<br/>

## 참고
https://victorydntmd.tistory.com/190

https://makinghome.tistory.com/67