# ﻿내일배움단 11일메이킹챌린지 3일차

## 백엔드 추가 작업



## 오늘 배운 어쩌구

### 특정 값이 어떤 목록 내에 있는지 확인하는 방법

- 목록을 튜플/집합으로 만들어 다음과 같이 검사한다.

```python
if 1 in (1,2,3,4):  # 튜플 (1, 2, 3, 4)의 원소 중 1이 있으면
    print("it works!")
    
if 1 in {1,2,3,4}:  # 집합 {1, 2, 3, 4}의 원소 중 1이 있으면
    print("it works!")
```



### 파이썬 작명 컨벤션

The [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html#316-naming) has the following convention:

> `module_name`, `package_name`, `ClassName`, `method_name`, `ExceptionName`, `function_name`, `GLOBAL_CONSTANT_NAME`, `global_var_name`, `instance_var_name`, `function_parameter_name`, `local_var_name`.

A similar naming scheme should be applied to a `CLASS_CONSTANT_NAME`	

[출처](https://stackoverflow.com/questions/159720/what-is-the-naming-convention-in-python-for-variable-and-function-names)

다음과 같이 요약 가능하다.

- LongName : 클래스, 익셉션
- LONG_NAME: 전역 상수 
- long_name : 그 외의 모든 이름들



### 값을 리턴하지 않는 함수들

파이썬은 변수의 값이 변화할 수 있으므로, 함수가 메세지 출력이나 리턴값 없이 객체의 값만 바꾸는 경우도 있다. 함수는 메소드를 호출한 객체, 메소드의 파라미터 객체의 값도 변화시킬 수 있단 것을 기억. 

(파이썬은 클로저와 달리 mutable data structures를 가짐)

```python
s1 =[1,2,3]
s2 =[4,5]

combo = s1.extend(s2)	# s2의 원소들이 모두 s1로 이동된다.

print(combo)      # 출력: None   
# extend 메소드는 주인과 대상의 값 자체를 변경시키고 아무 것도 리턴하지 않는다.

print(s1)		  # 출력: [1,2,3,4,5]
# s1로 s2의 원소들이 모두 이동하였다. 
```



### zip과 딕셔너리 생성

key 리스트와 value 리스트가 있을 때 다음과 같이 딕셔너리로 만들 수 있다,

```
name = ['merona', 'gugucon']
price = [500, 1000]

icecream = dict(zip(name, price))
print(icecream)
{'merona': 500, 'gugucon': 1000}
```

[출처](https://wikidocs.net/92539#zip)





## 참조

[레벨업 파이썬](https://wikidocs.net/book/4170)

[점프투파이썬](https://wikidocs.net/book/1)