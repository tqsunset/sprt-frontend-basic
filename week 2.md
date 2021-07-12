# 2주차 개발일지

## 1. jQuery
- JS를 그대로 사용하는 것의 단점 :코드가 복잡, 브라우저간 호환성 문제
- 따라서 일종의 '미리 작성된 JS코드'인 jQuery가 도입됨
- 사용하기 위해 import 코드가 필요
	```
	<head>
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
	</head>
	```
- 부트스트랩 코드는 jQuery를 사용 (부트스트랩 import 코드 자체에 포함되어있으므로 따로 import 필요 X) 
- jQuery의 효율성
	```
	document.getElementById("element").style.display = "none"; // JS로 작성 시

	$('#element').hide(); 				   	    // jQuery로 작성 시
	```  

## 2. 기초 jQuery 용법
- ```$('#아이디명')```으로 DOM 객체 선택
- ```Element.val()``` : arg. 없을 시 객체의 값 반환, arg. 있을 시 객체의 값을 arg.로 변환 	
	
	``` 
	\\ 객체의 값 구하기
	document.getElementById("element").val();

	$('#element').val();
	
	\\ 객체의 값 변경하기
	$('#element').val('장영실' );
	```
- ```Element.hide()``` ```Element.show()```: 객체를 숨김/보임
- ```Element.속성명()```: HTML 속성 값 반환

	``` 
	$('#btn-post-box').text(); 	//id가 btn-post-box인 요소(버튼)의 text 값(버튼 상의 문구)을 반환 
	$('#btn-post-box').text('포스팅박스 열기'); 	//id가 btn-post-box인 요소(버튼)의 text 값(버튼 상의 문구)을 '포스팅박스 열기'로 수정    
	```
- ```Element.css('속성명')```: css 속성 값 반환
	``` 
	$('#post-box').css('width'); 	//id가 post-box인 요소의 css 너비값을 반환 
	$('#post-box').css('width', '700px'); 	//id가 post-box인 요소의 css 너비값을 700px로 수정   
	```
- ```Element.append(\`HTML 코드\`)```: Element 내에 해당 HTML 요소를 삽입             (`:backtip)
   
- backtip으로 둘러싸인 스트링은 변수를 바로 삽입할 수 있다. `  ... ${변수명} ...`


- ```Element.val()```: Element가 input 요소일 때 사용자가 입력한 값을 반환 

- ```Element.append(string)```: Element 내부 끝부분에 string에 표현된 html 요소를 삽입한다.
	``` 
	\\ id가 names인 다음과 같은 <ul>이 있을 때
	\\ - Harrier Du Bois
	\\ - Kim Kitsuragi
	
	let name_html = '<li>Jean Viquemare</li>';
        $('#names').append(name_html)
        
          \\ 위의 코드 실행 시 마지막에 name_html이 추가된다.
	\\ - Harrier Du Bois
	\\ - Kim Kitsuragi
	\\ - Jean Viquemare
	```
- ```Element.empty()```: Element 내부의 내용을 모두 지운다. (Element 태그 자체는 유지)

- ```Element.remove()```: Element 태그 전체를 지운다. 

- ```Element.attr("속성명", "대체할 값")``` : Element의 속성Attribute을 수정한다.
	```
	<img id="img-cat" src="img/cat.png"/>
		
	//...
	
	$('#img-cat').attr("src", "img/dog.png)   // #img-cat 요소의 src 값을 변경
	```
- element.text() : element의 텍스트를 반환/변경
	```
	<p>달러-원 환율: <span id="rate">0</span></p>

	//...

	$('#rate').text('1137.5') // #rate인 span 요소의 텍스트가 0에서 1137.5로 변경 됨
	```
	
- 페이지가 로딩된 후 자동으로 실행되는 함수
	```
        $(document).ready(function () {  //페이지 로딩 후 아래의 코드들이 자동으로 실행된다. 
            updateRate()     
        });
	```
	
## 3. 기타 새로 배운 점
- 함수를 작성 시 alert나 console.log를 probe로 활용한다. 
- JS의 정규식은 /와 / 로 싸서 표현한다. e.g.) <b>/</b>\w+<b>/</b>   (클로저에서 "\w+"와 같음)
- 유용한 JS 함수
	- split() : regex를 인자로 받아 스트링을 여러개로 나눔 (배열 반환)
	- includes() : 어떤 문자열이 스트링에 존재하는지 확인 (참/거짓 반환)
 
 
## 4. Ajax
- Ajax는 jQuery가 임포트 된 파일에서 사용가능
```
$.ajax({
  	type: "GET", // GET 방식으로 요청한다.
  	url: "http://openapi.seoul.go.kr:8088/6d4d776b466c656533356a4b4b5872/json/RealtimeCityAir/1/99", // API endpoint
  	data: {}, // 요청하면서 함께 줄 데이터 (GET 요청시엔 비워두세요) - 파라미터?
  	success: function(response){ // 서버에서 준 응답을 response라는 변수에 담아 함수의 인자로 넘김
    	console.log(response) 		  // 함수의 본문. 서버에서 준 응답를 처리하는 부분. 
  	console.log(response['row'][0])  // 딕셔너리 형태인 response의 활용. 
  }
})
```


## 궁금한 부분
- td, tr에서 color를 설정하면 테이블 테두리까지 색상이 변한다. 텍스트 색상만 바꾸지 위해서는 어떻게 해야?
 내가 발견한 방안: 텍스트 색상을 바꾸고 싶은 tr/td에 대해 class css로 색상을 적용(테두리와 텍스트 모두 색상 적용) -> 해당 css문 하단에 tr/td의 스타일을 border: 1px solid black으로 설정(상단에서 하단 순으로 css문이 적용되면서 검은 테두리 색상 설정이 가장 나중에 적용된다)
 	```
        .underFive {   // 색상을 바꾸고 싶은 tr/td에 적용할 클래스 
            color: red;
        }

        td,
        th {
            border: 1px solid black;
        }
     	```
이 외에 더 간단한 방법이 있는지?

- API 리퀘스트 시 응답 본문을 변수에 저장하려고 아래와 같이 작성하면 cat에 헤더를 포함한 것으로 보이는 응답 전체가 저장된다. cat['responseJSON']을 통해 응답 분몬에 접근할 수 있음. 다른 식으로 접근하는 방법이 있는지?   
	```
	let cat = $.ajax({
			  type: "GET",
			  url: "https://api.thecatapi.com/v1/images/search",
			  data: {},
			  success: function(response){
				  console.log(response)
			  }}
			  
	  
	  let cat    // 두번째 시도, scope의 문제로 실행되지 않음
	  $.ajax({
	  type: "GET",
	  url: "https://api.thecatapi.com/v1/images/search",
	  data: {},
	  success: function(response){
		 cat = response // 응답 본문만 cat에 저장됨
	  }}
	  console.log(cat) // 응답함수 스코플를 벗어나 cat은 undefined로 돌아옴, 에러 발생
	    
	)
	```
    ! scope의 문제로 ajax() 괄호 바깥에서는 직접적으로 response에 접근할 수 없음, 첫번째 방법을 이용해 변수에 응답 전체를 저장 후 사용 가능한 듯 하다. -> 질문 시간에 확인 요
)
