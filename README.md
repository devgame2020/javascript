# javascript
# https://opentutorials.org/course/3085/18789



```javascript
// Array forEach사용하는법 
var arr = [ 'ab','de','fg','yy' ,'zz'];
arr.forEach((data,idx) => { console.log(idx +":" + data)} );
arr.forEach( function(data,idx) { console.log(idx +":" + data)} );
arr.forEach( (d,i) => console.log(i + ":" + d) );


// Array reduce
var arr = [ 1,2,3,4,5 ];
// a : 이전 리턴값
// d : data
// i : index 
var sum = arr.reduce(function(a,d,i) { 
    console.log(a,d,i);
    return a+d;
});

//-------------------------------------------------------------------------------------------------
// arr배열에서 2보다 큰 요소들만 추출하여 arr2에 넣는다.
var arr2 = arr.filter( (d,idx) => d>2);

let i=3;
a = ["100", "ryan", "music", "2"];
a.filter( function(a,b) { console.log(a,b); }); // 100 0 , ryan 1 , music 2,  2 3 이 출력됨
// i=3 이므로 2진수로 11임 
// filter로 , a배열의 0,2번째 항목이 추출됨
b = a.filter((d,idx) => i&(1<<idx)); // ["100", "ryan"]
b.join(""); // "100ryan"

// 이렇게 1줄로 처리가능
b = a.filter((d,idx) => i&(1<<idx)).join("");
//-------------------------------------------------------------------------------------------------

// Array map
const array1 = [1, 4, 9, 16];
const map1 = array1.map(x => x * 2);
// Array [2, 8, 18, 32]

// 
array1.map( function(x) { 
    console.log(x);
    return x;
});



// 배열의 모든 원소를 붙여서 1개의 String으로 변환
console.log(arr.join(''));

// a 를 int array형인 b로 변환
var a = "1,2,3,4";
var b = a.split(',').map(function(item) {
    return parseInt(item);
});

// array선언와 동시에 초기화
var arr = Array.from({length:5}, (data,idx)=>idx);
console.log(arr);
// 배열10개를 만들고 모두 1로 초기화
var arr2 = Array(10).fill(1);

// 배열의 정렬
let arr = [ 5,3,7,33,22,11,9 ];
// 오름차순 정렬
arr.sort( (a,b) => {
    let c = a-b;
    // b가 클경우 음수를 리턴하면 오름차순
    console.log(a,b,c);
    return c;
});
// 내림차순 정렬 
arr.sort( (a,b) => {
    let c = b-a;
    // b가 클경우 양수를 리턴하면 내림차순
    console.log(a,b,c);
    return c;
});


// 배열에서 최소값 구하기
var arr=[ 5,25,8,3,99,33];
var min = Math.min(...arr);  

// 배열에서 특정값제거
// arr배열에서 10을 찾아서 제거한다.
arr.splice(arr.indexOf(10),1);

// set 사용법
var set = new Set();
set.add(5);
set.add(1);
set.add(2);
set.add(1);
console.log(set);
var arr2 = [...set].sort((a,b)=>{return a-b;});
console.log(arr2);
```





# 동적계획법 과 분할정복 
* 동적계획법
    * 입력크기가 작은 부분문제들을 해결후, 해당부분 문제의 해를 활용해서, 보다 큰 크기의 부분문제를 해결하는방법
    * 상향식 접근방법
    * 메모이제이션(Memoization) 
* 분할정복
    * 문제를 나눌수없을때까지 나누어서 각각을 풀면서 다시 합병하여 문제의 답을 얻는 알고리즘
    * 하양식 접근법
 
* 공통점 : 문제를 잘개 쪼개서 분할함.
* 차이점 
    * 동적계획법
        * 부분문제는 중복되어, 상위문제해결시 재활용됨
    * 분할정복 
        * 부분문제는 서로 중복되지 않음. 

* 예시
    * 피보나치 수열 
        * F(n) = F(n-1) + F(n-2)
```javascript
function fibo(n) {
	if(n<=1) return n;
	return fibo(n-1) + fibo(n-2);
}

var a = fibo(10);
console.log(a);
```        


```javascript
function fibo_dp(n) {
	var arr = Array(n+1).fill(0);
	arr[0] = 0;
	arr[1] = 1;
	for(var i=2;i<=n;i++) 
		arr[i] = arr[i-1] + arr[i-2]
	return arr[n];
}
var a = fibo_dp(10);
console.log(a);
```

* 두수의 최대 공약수를 구하기
```javascript
    function gcd(w,h) {
        let mod = w%h;
        if(mod==0) return h;
        return gcd(h,mod);
    }
```    

* 두수의 최대 공배수를 구하기
(다른방법 : 두수를 곱한값 / 최대공약수)
```javascript
    function lcm(w,h) {
        let x = 0;
        while(true) {
            if(x%w == 0 && x%h==0) break;
            x++;
        }
        return x;
    }
```    










* 정규식 
```javascript
    var str = "100-200*300-500+20";
    // 수식에서 숫자제외한 연산자만 추출
    let sign = str.replace(/[0-9]/g,"").split("");
    console.log(sign);

    // 수식에서 숫자만 추출
    let num = str.split(/[^0-9]/g);
	num = num.map((it) => {
		return parseInt(it);
	});
    console.log(num);

    // 수식에서 숫자와 연산자를 분리하여  추출
    const arr = str.split(/(\D)/)
    console.log(arr);


    let a = "AB12CD";
    let reg=/[0-9]/g;
    a.match(reg); // 문자열a에서 숫자만 추출하여 배열로 만든다. [ "1", "2" ]
    a.indexOf(a.match(reg)[0]); // 해당 문자열에서 최초숫자 Index를 리턴한다. 숫자가 없으면 -1 


    let m = "CC#BCC#BCC#BX#CC#B";
    // 문자# (C#, X#)을 소문자 (c,x) 로 변환한다.
    m.replace(/(\D)#/g, (s,p1)=>p1.toLowerCase());
    // a : C# , b : C
    m.replace(/(\D)#/g, function(a,b) { console.log(a,b); return b;});
```    



