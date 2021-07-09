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
   
- `  ... ${변수명} ...`


