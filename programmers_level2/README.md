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


* 다리를 지나는 트럭
+ https://programmers.co.kr/learn/courses/30/lessons/42583


```javascript
// 내소스

function solution(bridge_length, weight, truck_weights) {
    var answer = 0;
    var bridge=[];


    function sumWeight(arr) {   
        return arr.length?arr.reduce( (p,d,i) => { return p+d; }):0;
    }
    
    function getTruckIdx(arr,sum) {
        if(bridge.length>=bridge_length) sum -= bridge[0];
        if(arr.length == 0) return -1;
        if(arr[0]+sum > weight) return -1;
        return 0;
    }
    
    for(;;) {
        let sum = sumWeight(bridge);
        let idx = getTruckIdx(truck_weights,sum);
        if(idx>=0) {
            bridge.push(truck_weights[idx]);
            truck_weights.splice(idx,1);
        }
        else {
            bridge.push(0);
        }
        
        if(bridge.length > bridge_length) 
            bridge.shift();            
     
        answer++;
        if(sumWeight(bridge) == 0 && truck_weights.length == 0) break;
    }
    
    return answer;
}
```

* 프린터
+ https://programmers.co.kr/learn/courses/30/lessons/42587?language=javascript


```javascript
// 내소스
function solution(priorities, location) {
    var answer = 0;
    for(;;) {
        var item = priorities.shift();
        if(Math.max(...priorities) > item) { 
            priorities.push(item); 
        }
        else {
            answer++;                    
            if(location == 0) break;
        }
        
        location--;
        if(location<0) location=priorities.length-1;
    }
    return answer;
}
```

* 124 나라의 숫자
+ https://programmers.co.kr/learn/courses/30/lessons/12899?language=javascript


```javascript
// 내소스(해결못함)
function solution(n) { 
    var answer = '';
  	var temp = n;
    var arr = ['4','1','2'];
 
    while(temp>0) {
        let idx = temp%3;
        answer = arr[idx] + answer;
        temp = Math.floor(temp/3) - (idx==0?1:0);
        
    }
    return answer;
}
```
   
***
***
   

