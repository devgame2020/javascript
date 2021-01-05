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
   


* 소수 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/42839?language=javascript


```javascript
// 내소스 (다른 소스 참고함)
function solution(numbers) {
    let answer = 0;
    let arr = [...numbers]; //numbers.split("");
    let k = 1;
    let i = 0;
    let store = [];

	// 모든경우의 수의 배열을 구한다.
	arr = recursion(arr);

	// 배열의 각각의 값들을 1~arr.length까지 잘라서 저장한다. (ex: 길이가 4라면 1,2,3,4)
	// array includes(num) : 배열이 num값을 포함하고 있는지 판별한다.
	for(let i=0;i<arr.length;i++) {
		for(let j=1;j<=arr.length;j++) {
			
			const num = parseInt(arr[i].slice(0,j));
			if(num>1 && !store.includes(num))
				store.push(num);
		}
	}

	// 오름차순 정렬
    store.sort((a,b) => a-b);

    answer = primeCheck(store);

    return answer;
}

function primeCheck(store){
	let max = Math.max(...store);
	// 소수 : 에라토스테네스의체
	var arr = [];
	for(let i=2;i<=max;i++) {
		if(arr[i] == null) {
			arr[i] = 1;
			for(let j=i*2;j<=max;j+=i) arr[j] = 0;
		}
	}
	
	// 
	let count=0;
	store.forEach( (d,i) => {
		if(arr[d])	 count++;
	});
	
	
	return count;
}

function recursion(arr,store=[],idx=0) {
	if(idx == arr.length-1) {
		store.push(arr.join(""));
		return;
	}
	for(let i=idx;i<arr.length;i++) {
		let tmp = arr[idx];
		arr[idx] = arr[i];
		arr[i] = tmp;
		
		recursion(arr,store,idx+1);
		
		arr[i] = arr[idx];
		arr[idx] = tmp;
	}
	
	return store;
}
```


* 카펫
+ https://programmers.co.kr/learn/courses/30/lessons/42842?language=javascript


```javascript
// 내소스 
function solution(brown, yellow) {
    var answer = [];
    for(let i=1;i<=yellow;i++) {
        if(yellow%i == 0) {
            let w = Math.max(i,yellow/i);
            let h = Math.min(i,yellow/i);
            let sum = (w+2)*(h+2);
            if(sum == (brown+yellow)) 
                return [w+2,h+2];
        }
    }
    return answer;
}
```



