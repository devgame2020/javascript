# javascript
# https://opentutorials.org/course/3085/18789



```
// forEach사용하는법 
var arr = [ 'ab','de','fg','yy' ,'zz'];
arr.forEach((data,idx) => { console.log(idx +":" + data)} );

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