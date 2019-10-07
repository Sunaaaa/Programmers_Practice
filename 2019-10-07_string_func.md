## String 함수 

- count()

  - 문자열에 있는 특정 문자 개수 세기

    ```python
    string = 'I love pizza and pasta'
    string.count('a')    # 4
    
    string = 'I love pizza and pasta'
    string.count('ve')    # 1
    ```

- index()

  - 문자열에 있는 특정 문자의 위치 알려주기

    ```python
    string = 'I love pizza and pasta'
    string.index('p')    # 7 
    ```

  - 해당 문자가 없는 경우 에러 발생!!

    ![1570460200562](https://user-images.githubusercontent.com/39547788/66323210-6445bb80-e95e-11e9-8e50-710048ad25ed.png)

  - 해결 방법 ==> find() 사용

    - 해당 문자가 문자열에 없으면 -1을 리턴한다. (에러 발생 X)

      ```python
      string = 'I love pizza and pasta'
      string.find('q')    # -1
      ```

    
