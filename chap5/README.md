# 변수와 대입 연산자

+ var a = 2;
+ var a = "aaa";
+ var a = 'aaa';
+ var a = true;
+ var a = [];
+ var a = {};
+ var a = undefined;

# ES6 새로운 변수 선언 방식 - const, let

+ let sum = 0;
    + block단위로 변수의 범위가 제한된다. (지역변수)
    + 한번 선언한값에 대해서 다시 선언할수없다. 

+ const a = 10;
    + 한번 선언한 값을 변경할수없다 (상수개념)
    + a = 20; // Error

+ 비교 연산자
    + 비교는 == 보다는 === 를 사용한다.
        + === 의 경우는 type까지 확인한다.
    + == 는 임의적으로 type을 바꿔서 비교한다.
        + 0 == false; // true
        + "" == false; // true 
        + null == false; // false (null은 객체)
        + undefined == false; // false 
        + 0 == "0"; // true
        + null == undefined; // true 


