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



