# 3주차 개발일지

## 1. 웹페이지에 오픈 API 적용하기

- API 응답의 자료를 사람이 직접 처리하는 과정을 거치지 않고 그대로 웹페이지에 적용할 수 있다.

  ```javascript
  <script> 
      
  	$(document).ready(function () {
              listing();									// 페이지가 로딩된 직후 function(){ }를 실행한다.
          })
          
  	function listing() {
              //console.log('화면 로딩 후 잘 실행되었습니다');  //prob4
  
              $("#card-columns").empty();					// 먼저 API컨텐츠를 넣을 div를 비움.
  
              $.ajax({										// Ajax API 리퀘스트
                  type: "GET",
                  url: "http://spartacodingclub.shop/post",
                  data: {},
                  success: function (response) {
                      let articles = response['articles']			// 응답에서 article 키의 값을 변수 article에 저장 
                      //console.log(articles)						// prob
                      
                      for (let i = 0; i < articles.length; i++) {	// for문을 이용한 반복
                          let comment = articles[i]['comment']	// article 원소의 값들을 각자 저장 
                          let desc = articles[i]['desc']
                          let image = articles[i]['image']
                          let title = articles[i]['title']
                          let url = articles[i]['url']
                          // console.log(title, desc, image, comment, url)	//prob
  
                          let temp_html = `<div class="card">
                                                  <img class="card-img-top"
                                                       src="${image}"
                                                       alt="Card image cap">
                                                  <div class="card-body">
                                                      <h5 class="card-title"><a href="${url}">${title}</a></h5>
                                                      <p class="card-text">${desc}</p>
                                                      <p class="card-comment">${comment}</p>
                                                  </div>
                                              </div>` 			// article 원소들의 값과 html 골격을 이용하여 temp_html 작성
  
                          $("#card-columns").append(temp_html)	// #card-colums 요소에 temp_html을 붙이고 for문으로 돌아감
                      }
  
                  }
              })
  
          }
  </script>
  ```

  

## 2. Python 기본

- 프로젝트 생성

  ![](/home/gwlee/Pictures/Screenshot from 2021-07-14 16-07-25.png)

  - Environment location 주소의 마지막이 venv 폴더로 되는지 확인 (이유?)
  - Create a main.py welcome script 역할?

- 프로젝트 실행 :  Shift + Ctrl + F10 (또는 에디터 창 오른클릭 후 Run)

- 변수 선언 : 자료형에 상관없이 `(변수명) = (값)`

  ```python
  a = 1
  b = 3
  
  print(a+b) # 4를 출력
  ```

- Exception handling

  ```python
  # variable
      
  a = 1
  b = 3
  first_name = 'Kim'
  
  print(a+first_name)
  
  # 에러 메세지
  Traceback (most recent call last):
    File "/home/gwlee/PycharmProjects/pythonPrac/hello.py", line 7, in <module>  # 에러가 발생한 라인 지적
      print(a+first_name)
  TypeError: unsupported operand type(s) for +: 'int' and 'str'					# 에러의 이유
  ```

  

- 주요 자료형과 함수

  ```python
  # 1. 리스트
  
      a_list = [1, 2, 3, 4]
  
      # 리스트 요소 접근 방법: JS와 동일
      a_list[0]				
  
      a_list.append('hey')	# 리스트 요소 추가, [1, 2, 3, 4, 'hey'], 뒤에 추가되며 자료형 무관
  
  # 2. 딕셔너리
      a_dict = {}
      a_dict = {'name':'bob','age':21}
      a_dict['height'] = 178
  
      # a_dict의 값은? {'name':'bob','age':21, 'height':178}
      # a_dict['name']의 값은? 'bob'
  
      
  ```

  - tuple과 set 자료형, class는 현 강의에선 다루지 않음

- 함수 선언: `def`

  ```python
  def addition (num1, num2):
  	print('Hey!')
      return num1 + num2 	
  
  # 함수 본문은 들여쓰기로 구분
  ```

  

- 조건문: `if : ... else: ...` 

  ```python
  if age > 20:
  	print('성인입니다')
  else:
  	print('청소년입니다')
  ```

- 반복문: `for ... in ...`

  ```python
  fruits = ['사과','배','배','감','수박','귤','딸기','사과','배','수박']
  
  count = 0
  for fruit in fruits:
  	if fruit == '사과':
  		count += 1
  
  print(count)
  
  # 사과의 갯수를 세어 보여줍니다.
  ```

- 주요 함수

  ```python
  str(2)  # 숫자를 스트링으로 변경
  ```



## 3.  파이썬 패키지의 사용

- 파이썬 프로젝트는 각자의 가상환경(패키지/라이브러리 환경)을 가지고 있다. 타 프로젝트 및 타 파이썬 어플리케이션과 격리된 실행환경으로, 같은 시스템에서 실행되는 다른 파이썬 프로그램들의 동작에 영향을 주지 않는다.

- 파이썬 패키지 설치 방법: pip(파이썬 패키지 관리자)을 사용, 앱을 설치할 때 앱스토어를 사용하는 것과 유사

  -  Settings - project interpreter 화면(상단 이미지)에서 + 버튼을 누르면 뜨는 창에서(하단 이미지) 대상 패키지를 검색 후 설치

  ![](/home/gwlee/sparta-beginner/sprt-frontend-basic/img/week03-1.png)

  ![](/home/gwlee/sparta-beginner/sprt-frontend-basic/img/week03-2.png)

  

## 4. beautifulsoup 패키지를 이용한 크롤링

- ##### 크롤링(웹스크래핑)
  
  1. http 리퀘스트를 생성
  2. 응답 html에서 필요한 부분을 parsing, 추출하는 과정
  
- beautifulsoup: 크롤링의 2번과정, 필요한 부분을 추출하는 기능을 보조하는 라이브러리

### beautifulsoup 기본 사용 설정

다음 예시를 보자.

```python
import requests
from bs4 import BeautifulSoup

# 1. 브라우저에서의 접근으로 가장하기 위한 header
headers = {'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.86 Safari/537.36'}

# 2. 헤더와 타겟URL을 가지고 GET 리퀘스트 생성, 응답을 data에 저장  
data = requests.get('https://movie.naver.com/movie/sdb/rank/rmovie.nhn?sel=pnt&date=20200303',headers=headers)

# 3. 리퀘스트 응답 parsing
# HTML을 BeautifulSoup 라이브러리를 통해 검색하기 용이한 상태로 만듦
# soup이라는 변수에 "파싱 용이해진 html"이 담긴 상태가 됨
soup = BeautifulSoup(data.text, 'html.parser')

# 4. soup 변수의 메소드 select, select_one을 사용하여 데이터 추출이 가능
```

- ##### 사용된 주요 메소드

  1. **requests.get**(url)  
     - requests 라이브러리 
     - GET 요청 시 사용
     - [자세한 사용방법 정리](https://dgkim5360.tistory.com/entry/python-requests) 
  2. **BeautifulSoup**(html_string, parsing_type)
     - arg. : *HTML 도큐먼트 str*, *parsing 방법*(e.g. `'html.parser'`) 
     - 해당 html 문서를 parsing하여  BeautifulSoup 객체로 만든 후 리턴
     - html 문서 내의 DOM 구조가 객체 내부에 그대로 반영되어있음 -> 특정 위치/조건의 DOM을 탐색 가능



- #### 메소드 select, select_one

    - **select**(): 해당하는 DOM의 배열을 반환
    
    - **select_one**(): 해당하는 DOM을 하나만 반환
    
        ```python
        # 선택자를 사용하는 방법 (copy selector)
        soup.select('태그명')
        soup.select('.클래스명')
        soup.select('#아이디명')
        
        soup.select('상위태그명 > 하위태그명 > 하위태그명')
        soup.select('상위태그명.클래스명 > 하위태그명.클래스명')
        # 예시) soup.select('#old_content > table > tbody > tr')
        
        # 태그와 속성값으로 찾는 방법
        soup.select('태그명[속성="값"]')
        
        # 한 개만 가져오고 싶은 경우
        soup.select_one('위와 동일')
        ```
    
        기본 사용설정 예시에서 이어지는 코드가 다음과 같다고 하자.
    
        ```python
        movies = soup.select('#old_content > table > tbody > tr')  # (1)
        
        for movie in movies:
            # movie 안에 a 가 있으면,
            a_tag = movie.select_one('td.title > div > a')   	   # (2)
            if a_tag is not None:
                # a의 text를 찍어본다.
                print (a_tag.text) 								   # (3)
        ```
    
        - (1) 변수 movies에 `#old_content > table > tbody > tr`에 해당하는 모든 DOM 배열을 저장
        - (2) 각 tr 요소마다 `td.title > div > a`인 a 요소들을 추출하여 변수 a_tag에 저장, tr 안에 a 요소가 존재하지않는 경우엔 `None`이 저장된다.
        - (3) a_tag에 저장된 a 요소가 None이 아닌 경우(타겟 요소가 존재하는 경우) 해당요소의 텍스트를 출력한다.
    
        따라서 이 코드는 대상 문서에서 `#old_content > table > tbody > tr > td.title > div > a`인 모든 a 요소들의 텍스트만을 선택해서 추출함을 알 수 있다.
    
    - **DOM의 속성/텍스트 추출**
    
      - `태그['속성']` : 해당 태그 요소의 속성 반환
      
      - `태그.text` : 해당 태그 요소의 텍스트 반환
      
        

> ##### ❗선택자 selector
>
> `#old_content > table > tbody > tr`와 같이 html 문서 내에서 특정 요소의 위치를 알려주는 경로를 선택자라고 한다. (파일 경로와 유사) 
>
> 타겟 요소의 선택자는 크롬 개발자도구를 통해 알 수있다. (항상 정확하진 않음)
>
> 1. 원하는 부분에서 마우스 오른쪽 클릭 → 검사
> 2. 원하는 태그에서 마우스 오른쪽 클릭
> 3. Copy → Copy selector로 선택자를 복사할 수 있음
>
> ![](/home/gwlee/sparta-beginner/sprt-frontend-basic/img/Untitled.jpg)



> ❗타겟 태그들에 접근하는 순서/전략은 다양할 수 있고, 상황에 따라 효율적인 방식이 다르다.



## 5. MongoDB

- 설치 : [MongoDB 설치/실행 관련 도큐먼테이션](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)

- 실행

  ```shell
  $ sudo systemctl start mongod
  # alias 설정으로 단축해서 사용하면 편리하다.
  ```

- **Robo3T** : MongoDB의 GUI 어플리케이션, DB 내용을 확인하기 편리함
- **pymongo**: 파이썬 언어로 MongoDB를 조작할 수 있게 해주는 라이브러리

  

#### 데이터베이스의 두 종류

![](/home/gwlee/sparta-beginner/sprt-frontend-basic/img/db.png)

1. ##### SQL 

   - 컬럼 항목들이 데이터베이스의 생성 시 결정됨, 컬럼 설계의 필요성
   - 운영 중 컬럼 변경이 어려움
   - 대신 데이터가 일관적이며 분석이 빠름 

2. ##### NoSQL

   - Not only SQL
   - 컬럼이 정해져 있지않음, 딕셔너리(맵)의 집합이며 데이터마다 키 값이 다를 수 있음
   - 데이터가 각각 독립된 딕셔너리이므로 운영 중 컬럼 수정이 SQL보다 용이함

   => MongoDB는 NoSQL에 속한다.

   

#### MongoDB의 구조

![](/home/gwlee/sparta-beginner/sprt-frontend-basic/img/mongodb-structure.jpg)

- 좌측이 SQL(RDBMS), 우측이 MongoDB의 구조이다.
- SQL이 데이터베이스 - 테이블 - 열 - 칼럼 순의 구조인 것처럼 NoSQL에서는 동일한 구조를 가지지만 이름만 다르다.
- MongoDB: 데이터베이스 - 콜렉션 - 도큐먼트 - 필드
- CRUD 메소드 사용 시 `대상DB.대상콜렉션.메소드()`의 순으로 대상을 특정해준다.  



#### pymongo를 통한 CRUD

- CREATE에는 `insert`, READ는 `find`,  UPDATE는 `update`, DELETE는 `delete` 메소드를 사용한다.

- **삽입 (insert)**

  - `db.collection.insert_one(dict)` : 하나의 딕셔너리를 database에 추가.

  ```python
  from pymongo import MongoClient           # pymongo를 임포트
  client = MongoClient('localhost', 27017)  # mongoDB는 로컬 27017 포트로 작동
  db = client.dbsparta                      # 'dbsparta'라는 이름의 데이터베이스를 불러오고, 없으면 새로 생성함.
  
  # MongoDB에 insert 하기
  
  db.users.insert_one({'name':'bobby','age':21})
  db.users.insert_one({'name':'kay','age':27})
  db.users.insert_one({'name':'john','age':30})
  ```

  

- **조회(read)** 

  - `list(db.collection.find(검색조건 dict,표시 키 dict))`: 검색조건에 맞는 데이터들에서 표시 키 dict에 해당하는 키값만 리턴.

    - <u>검색조건 dict</u> 

      예) `{'age':21}` 나이가 21인 데이터들을 모두 찾음

    - <u>표시 키 dict</u> 

      예) `{'_id':False} ` 모든 키의 표시 여부는 true로 기본 설정되어있고, 보지 않을 항목 '_id'만 False로 설정하여 출력 결과에 포함되지 않도록 함.

      > ❗find()의 결과물은 pymongo 객체일뿐 이다. list( ) 함수로 한번 처리하여야 데이터 리스트를 얻을 수있다.


  ```python
  # MongoDB에서 데이터 모두 보기
  all_users = list(db.users.find({}))
  
  # MongoDB에서 특정 조건의 데이터 모두 보기
  same_ages = list(db.users.find({'age':21},{'_id':False}))
  
  print(all_users[0])         # 0번째 결과값을 보기
  print(all_users[0]['name']) # 0번째 결과값의 'name'을 보기
  ```

  

  - `db.collection.find_one()`: 검색 조건에 맞는 데이터 <u>하나만</u> 반환, find와 같은 arg.를 가짐

  ```python
  user = db.users.find_one({'name':'bobby'})
  print(user)
  ```

  

- **수정 (update)**

  - `db.collection.update_one(찾을조건 dict,{ '$set': 변경 내용 dict })`

  ```python
  db.users.update_one({'name':'bobby'},{'$set':{'age':19}})
  
  # db.users.update_many()도 있어서 여러 데이터를 한번에 수정 가능하나 위험함, 자주 사용되지 않음
  ```

- **삭제 (delete)**:

  - `db.collection.delete_one(찾을조건 dict)`

  ```python
  db.users.delete_one({'name':'bobby'})
  
  # db.users.delete_many()도 있어서 여러 데이터를 한번에 수정 가능하나 위험함, 자주 사용되지 않음
  ```



# 6. 웹스크래핑 결과 DB 저장

```python
import requests
from bs4 import BeautifulSoup
from pymongo import MongoClient

# http 응답 얻고 적당한 parsing으로 리스트 구하기
headers = {'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.86 Safari/537.36'}
data = requests.get('https://movie.naver.com/movie/sdb/rank/rmovie.nhn?sel=pnt&date=20200303',headers=headers)
soup = BeautifulSoup(data.text, 'html.parser')
trs = soup.select('#old_content > table > tbody > tr')

# MongoDB와 연결하고 대상 데이터베이스를 찾음 
client = MongoClient('localhost',27017)
db = client.dbsparta

# 반복문을 이용하여 리스트의 요소마다 필요한 정보를 parsing한다. 
for tr in trs:
    titles = tr.select_one('td.title > div > a')
    points = tr.select_one('td.point')
    if titles is not None:	
        title = titles.text
        point = points.text
        movie = {					# parse된 정보를 딕셔너리 형태로 만든다.
            'title': title,
            'point': point	
        }
        db.movies.insert_one(movie)	# 생성된 딕셔너리를 이 데이터베이스의 movies 콜렉션에 추가한다.
        print(title, point)			# (prob역할)	
```
