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
// b : data
// c : index 
var sum = arr.reduce(function(a,b,c) { 
    console.log(a,b,c);
    return a+b;
});

// Array map
const array1 = [1, 4, 9, 16];
const map1 = array1.map(x => x * 2);
// Array [2, 8, 18, 32]


// 배열의 모든 원소를 붙여서 1개의 String으로 변환
console.log(arr.join(''));

// array선언와 동시에 초기화
var arr = Array.from({length:5}, (data,idx)=>idx);
console.log(arr);

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



