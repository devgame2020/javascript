# 프로그래머스 코딩 테스트 Level 2

* 기능개발
+ https://programmers.co.kr/learn/courses/30/lessons/42586


```javascript
// 내소스
function solution(progresses, speeds) {
    var answer = [];
    var arr = [];
    progresses.forEach( (d,i) => { arr.push(Math.ceil((100-d)/speeds[i])); } );
    for(var i=1,d=arr[0],fin=1;i<arr.length;i++) {
        if(d>=arr[i]) fin++;
        else { answer.push(fin); fin=1; d=arr[i] }
    }
    answer.push(fin);
    
    return answer;
}
```

   
***
***
   

