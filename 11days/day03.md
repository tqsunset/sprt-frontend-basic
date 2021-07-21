

```python
if 1 in (1,2,3,4):  # 튜플 (1, 2, 3, 4)의 원소 중 1이 있으면
    print("it works!")
    
if 1 in {1,2,3,4}:  # 집합 {1, 2, 3, 4}의 원소 중 1이 있으면
    print("it works!")
```





파이썬 작명 컨벤션

The [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html#316-naming) has the following convention:

> `module_name`, `package_name`, `ClassName`, `method_name`, `ExceptionName`, `function_name`, `GLOBAL_CONSTANT_NAME`, `global_var_name`, `instance_var_name`, `function_parameter_name`, `local_var_name`.

A similar naming scheme should be applied to a `CLASS_CONSTANT_NAME`



list.extend()

```python
s1 =[1,2,3]
s2 =[4,5]

combo = s1.extend(s2)	# s2의 원소들이 모두 s1로 이동된다.

print(combo)      # 출력: None   
# extend 메소드는 주인과 대상의 값 자체를 변경시키고 아무덕도 리턴하지 않는다.

print(s1)		  # 출력: [1,2,3,4,5]
# s1로 s2의 원소들이 모두 이동하였다. 
```





참조

https://stackoverflow.com/questions/159720/what-is-the-naming-convention-in-python-for-variable-and-function-names

