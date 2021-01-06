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



* 가장 큰 수
+ https://programmers.co.kr/learn/courses/30/lessons/42746?language=javascript


```javascript
// 내소스 
function solution(numbers) {
    const answer = numbers.sort((a, b) => {      
        let aa = parseInt(""+a+b);
        let bb = parseInt(""+b+a);
        
        if (aa < bb) return 1;
        if (aa > bb) return -1;
        return;
    }).join('');    
    
    var i;
    for(i=0;i<answer.length-1;i++) { 
        if(answer[i] != "0")  
            break;  
    }
    
    return answer.substring(i);
}
```


```javascript
// 다른사람 소스
function solution(numbers) {
    var answer = numbers.map(v=>v+'')
                        .sort((a,b) => (b+a)*1 - (a+b)*1)
                        .join('');

    // 맨앞이 0이면 그 뒤의 숫자들은 무조건 "0"이다.
    return answer[0]==='0'?'0':answer;
}
```


* H-Index
+ https://programmers.co.kr/learn/courses/30/lessons/42747?language=javascript


```javascript
// 내소스 
function solution(citations) {
    var answer = 0;
    citations.sort( (a,b) =>{
       return b-a; 
    });

    for(;answer<citations.length;answer++) {
        if(answer>=citations[answer]) break;
    }
    return answer;
}
```


   
***
***
   



* 다음 큰 숫자
+ https://programmers.co.kr/learn/courses/30/lessons/12911?language=javascript


```javascript
// 내소스 
function solution(n) {
    var answer = 0;
    let cnt = 0;
    [...n.toString(2)].forEach( (d) =>{ cnt+=parseInt(d); });
    for(var i=n+1;;i++) {
        let sum=0;
        [...i.toString(2)].forEach( (d) =>{ sum+=parseInt(d); });
        if(sum == cnt) {
            answer = i;
            break;
        }
    }
    
    return answer;
}
```





* 최솟값 만들기
+ https://programmers.co.kr/learn/courses/30/lessons/12941?language=javascript


```javascript
// 내소스 (시간초과)
function recursion(B,arr,num=Number.MAX_VALUE,idx=0) {
    if(idx == arr.length-1) {
        let sum=0;
        for(let x=0;x<B.length;x++) 
            sum += (arr[x]*B[x]);
        if(num>sum) num=sum;
        return num;
    }    
    
    for(let i=idx;i<arr.length;i++) {
        let tmp = arr[idx];
        arr[idx] = arr[i];
        arr[i] = tmp;
        
        let num2 = recursion(B,arr,num,idx+1);
        if(num2<num) num=num2;
        
        arr[i] = arr[idx];
        arr[idx] = tmp;
    }
    return num;
}

function solution(A,B){
    var answer = 0;
    answer = recursion(B,A);
    return answer;
}
```


```javascript
// 내소스 (통과됨) 
// A는 오름차순, B는 내림차순으로 정렬후 서로 곱한다.
function solution(A,B){
    var answer = 0;
    A.sort((a,b) => { return a-b });
    B.sort((a,b) => { return b-a });    
    A.forEach( (d,i) => answer+=(d*B[i]));
    return answer;
}
```


```javascript
// 다른사람소스 
function solution(A,B){
    A.sort((a, b) => a - b)
    B.sort((a, b) => b - a)
    return A.reduce((total, val, idx) => total + val * B[idx], 0)
}
```


* 피보나치 수
+ https://programmers.co.kr/learn/courses/30/lessons/12945?language=javascript


```javascript
// 내소스 
function solution(n) {
    var answer = 0;
    var n0 = 1;
    var n1 = 1;
    var n2 = 0;
    for(let i=2;i<n;i++) {
        let sum=n0+n1;
        n2 = n1;
        n1 = n0;
        n0 = sum % 1234567;
    }
    answer = n0;
    
    return answer;
}
```



* 최댓값과 최솟값
+ https://programmers.co.kr/learn/courses/30/lessons/12939?language=javascript#


```javascript
// 내소스
function solution(s) {
    var answer = '';    
    const arr = s.split(" ");
    let min = Math.min(...arr);
    let max = Math.max(...arr);
    answer = min + " " + max;
    return answer;
}
```


```javascript
// 다른사람소스
function solution(s) {
    const arr = s.split(' ');

    return Math.min(...arr)+' '+Math.max(...arr);
}
```


   
***
***
   



