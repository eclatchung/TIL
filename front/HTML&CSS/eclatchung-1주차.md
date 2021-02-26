# HTML 
## HTML
> HTML (HyperText Markup Language)<br>
 : 하이퍼 텍스트를 가장 중요한 특징으로 하는 마크업이라는 형식을 가진 컴퓨터 프로그래밍 언어

- a.html 
    + a : 파일 이름
    + html : 확장자명
- 웹페이지는 HTML 문서라고도 불린다.
- HTML 태그들로 구성이 된다.
- HTML의 최신버전은 HTML5 => ```<!DOCTYPE html>```
- W3C에서 관리 (웹표준 제정, 관리하는 중립적인 기관)

<br>

## HTML 문법 
### 1. 태그
1. HTML 태그는 HTML 요소라고도 부르며, HTML 문서를 구성하는 기본 단위이다.
2. 각각의 HTML 태그는 웹페이지의 디자인이나 기능을 결정하는데 사용된다.
3. HTML 태그는 태그 이름을 꺾쇠 괄호로(<>) 감싸서 표현합니다.
```
<태그이름> : 시작 태그
</태그이름> : 종료 태그 => 빈태그들은 종료 태그 없어도 됨 
(빈태그  :  <img><br><hr> 등 )
```

### 2. 기본 구조 

````html
<!DOCTYPE html> // 현재 문서가 HTML5임을 명시
<html> // HTML 문서의 루트 요소 정의
    <head> // HTML 문서의 메타데이터를 정의
    <title> 문서의 제목 </title> // HTML 문서의 제목을 정의
    </head>
    <body> // 웹브라우저를 통해 보이는 내용 부분
    ...
    </body>
</html>

````
``` metadata```
- 문서에 대한 정보로 웹브라우저에는 직접벚ㄱ으로 표현되지 않는 정보이다. 
-  < title >, < style >, < meta >, < link >, < script >,< base >태그 등 ..

```<title>```
- 웹브라우저의 툴바에 표시 
- 웹브라우저의 즐겨찾기에 추가할때 즐겨찾기의 제목
- 검색 엔진의 결과 페이지에 제목으로 표시  

### 3.속성
속성
- 태그이름만으로는 정보가 불충분함
- 속성으로 태그의 정보 더함.

### 4. 태그의 중첩과 목록


```<ol>, <ul>, <li>```
1. ```<ol>```
    - ordered list
    - 순서 있는 리스트
2. ```<ul>```
    - unordered list
    - 순서 없는 리스트
3. ```<li>```
    - 리스트 
    - ```<ol>```와 ```<ul>``` 안의 리스트 

```html
<ol>
    <li> 리스트 1 </li>
    <li> 리스트 2 </li>
</ol>

<ul>
    <li> 리스트 1 </li>
    <li> 리스트 2 </li>
</ul>

```

### 5. 단락 ```<p>```
단락이란 내용상 끊어서 구분할 수 있음
=> 띄어쓰기나 줄 나누기 영향 없음

- ```<br>``` 태그 사용시 새로운 단락 생성 하지 않고 줄을 나눌 수 있음
- ```<hr>``` 태그 사용시 단락 나누거나 구분표현 가능
- ```<pre></pre>```태그 사용시 HTML 코드에서 작성한 텍스트 서식 그대로 표시 가능

### 6. 이미지 ```<img>```
이미지 삽입시 ```<img>``` 태그
```<img src="이미지주소" alt="대체 문자열">```
- 이미지 스타일 정의
    1. css
    ``` html
    <style>
    img{
        width : 100%
        boader :1 px solid black
    }
    </style>
    ```
    2. 
     ``` html
    <img src ="~" width = "" height ="">
    ```
    3.
     ``` html
    <img src ="~" stype="width:320px,height:214px">
    ```

### 7. 링크
```<a>```
- anchor의 약자
- href 속성으로 url을 입력하면 해당 url의 링크로 이동

### 8. ```<table>```
1. ```<tr>``` : 열구분
2. ```<th>``` : 각열의 제목 ( 굵은 글씨, 가운대 정렬 )
3. ```<td>``` : 테이블 열 

 ``` html
    <table>
        <tr>
            <th>
                제목1
            </th>
            <th>
                제목2
            </th>
        </tr>
        <tr>
            <td>
                1셀
            </td>
        </tr>
        <tr>
            <td>
                2셀
            </td>
        </tr>
    </table>
```

- 속성
    - colspan = "숫자" : 열 합침
    - rowspan = "숫자" : 행 합침

### 9. ```<form>```
- 사용자 입력

```<form action="처리할 페이지 주소" method="get|post" > </form>```


- 속성
    1. action : 입력 받은 데이터를 처리할 서버상의 스크립트 파일구조
    (해당 파일 구조는 form-handler라고 한다.)
    2. method  : GET 또는 POST 방법 중 하나로 데이터를 보낸다.
        - GET : 주소에 데이터 추가 전달.
        - POST : 별도 첨부하여 전달
        - 보안성 :  POST > GET

#### ```<input>```

- ```<input>```요소 (type)
    1. text : 문장 한줄
    2. password : 비밀번호
    3. radio 
        - input의 name 이 같아야함
        - checked : 미리 체크
        - value : 라디오의 값
    4. checkbox
        - checked : 미리 체크
        - disabled : 선택 불가
    5. file
        - accept : 받을 파일 확장자 종류 명시
    6. select
        ````html
            <select name = "fruit">
                <option value = "apple">사과
                <option value ="banna"> 바나나
            </select>
            
        ```
    7. textarea : 여러줄
        - 크기 rows, cols 속성
    8. button
        - onclick = "클릭했을 때의 이벤트"
    9. submit
        - 폼 핸들러로 데이터 전송
    10. ```<fieldset>```
        - form 요소와 관련된 데이터를 하나로 묶음
        - ```<legend>``` : filedset의 제목

- 속성
    - value : 초깃값
    - readonly : 고정값, 볼 수 는 있으나 수정은 할수 없음
    (disable 과 다른점 : 전송시 readonly는 초깃값 전송, disable은 값 전달 하지 않음)