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

// arr배열에서 2보다 큰 요소들만 추출하여 arr2에 넣는다.
var arr2 = arr.filter( (d,idx) => d>2);

// Array map
const array1 = [1, 4, 9, 16];
const map1 = array1.map(x => x * 2);
// Array [2, 8, 18, 32]


// 배열의 모든 원소를 붙여서 1개의 String으로 변환
console.log(arr.join(''));

// array선언와 동시에 초기화
var arr = Array.from({length:5}, (data,idx)=>idx);
console.log(arr);
// 배열10개를 만들고 모두 1로 초기화
var arr2 = Array(10).fill(1);


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