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

```javascript
// 내소스, 2022-02-21
function solution(progresses, speeds) {
    var answer = [];
    var fin = [];
    progresses.forEach( (d,i) => {
        fin.push(Math.ceil((100-d)/speeds[i]));
    });

    var build_time = 0;
    var cnt = 0;
    fin.forEach( (d,i) => {
        if(build_time >= d) cnt++;
        else {
            if(cnt>0) answer.push(cnt);
            cnt = 1;
            build_time = d;
        }
    });    
    if(cnt>0) answer.push(cnt);
    
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


```javascript
// 내소스(해결못함), 2022-02-17
class Solution {
    public String solution(int n) {
        StringBuffer answer = new StringBuffer();
        while(n>0) {
            int mod = n%3;
            answer.append((mod==0?4:mod));
            n = n/3 - (mod==0?1:0);
        }
        return answer.reverse().toString();
    }
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
   


* 위장
+ https://programmers.co.kr/learn/courses/30/lessons/42578?language=javascript


```javascript
// 내소스
// 각 종류+1 을 모두 곱한후에 1을 빼면 된다. 
function solution(clothes) {
    var answer = 1;
    var arr = [];
    // map에 각각의 옷을 넣는다.
    var mMap = new Map();
    clothes.forEach( (d,i) => {
        if(!mMap.get(d[1])) 
            mMap.set(d[1], [ d[0] ]);
        else
            mMap.get(d[1]).push(d[0]);
    });

    // 각각의 타입의 갯수를 배열에 넣는다.
    var arr2 = [];    
    for(let [key,value] of mMap) {
        arr2.push(value.length);
    }
    
    arr2.forEach( (d,i) => {
       answer *= (d+1);
    });
    answer--;
    return answer;
}
```

* 소수 만들기
+ https://programmers.co.kr/learn/courses/30/lessons/12977?language=javascript


```javascript
// 남의소스
function isPrime(num) {
    for(let i=2;i<num;i++)
        if(num%i == 0) return false;
    return true;
}

function solution(nums) {
    var answer = 0;
    
    // 배열에서 3개씩 추출한다.
    let len = nums.length;
    for(let i=0;i<len;i++) {
        for(let j=i+1;j<len;j++) {
            for(let k=j+1;k<len;k++) {
                let num = nums[i] + nums[j] + nums[k];
                // 소수인지 체크한다.
                if(isPrime(num)) answer++;
            }
        }
    }
    
    return answer;
}
```


* 올바른 괄호
+ https://programmers.co.kr/learn/courses/30/lessons/12909?language=javascript


```javascript
// 내소스
function solution(s){
    var answer = true;
    var stack = [];
    [...s].forEach( (d) => {
        if(d == "(") stack.push(d);
        if(d == ")") {
            if(stack.pop() === undefined) answer = false;
            
        }
    });
    if(stack.length>0) return false;

    return answer;
}
```

* 큰 수 만들기
+ https://programmers.co.kr/learn/courses/30/lessons/42883?language=javascript


```javascript
// 다른사람소스 
function solution(number, k) {
    var answer = '';

    var stack = []; 
    for (var i = 0; i < number.length; i++) { 
        var now = number[i]; 
        // 이번에 입력받은값 now가 현재 스택에 있는값보다 크면 해당 값을 제거한다.
        // K가 0이 될때까지 제거하거나, now보다 큰값일때까지 반복한다. 
        while (k > 0 && stack[stack.length - 1] < now) {
            stack.pop();
            k--;
        }
        stack.push(now);
    }

    stack.splice(stack.length - k, k);
    answer = stack.join('');
    return answer;    
}
```



   
***
***
   


* 조이스틱
+ https://programmers.co.kr/learn/courses/30/lessons/42860?language=javascript


```javascript
// 다른사람소스
// "BBBBAAAB" ==> 10 (12가 나옴)
// 해당 소스는 통과는 되었지만, 틀린경우도 있음.
// "AAAA" => 0 (-2가 나옴)
function solution(name) {
    const arr = [0];

    const answer = [...name].reduce((answer, s, i)=>{
        if(s === "A"){
            // 현재 문자가 A인데, 이전문자가 A가 아니라면, 연결된 문자의 갯수를 구해서 push한다.
            if(name[i-1]!= "A") arr.push(continuous(name.substring(i))-(i-1));
            return answer + 1;
        }    
        return answer + ascii(name, i) + 1;
    }, 0);

    // 
    return answer - Math.max(...arr) -1;
}

function ascii(name, i){
    const num = name.charCodeAt(i);
    return (num > 78)? 91 - num : num - 65;
}

function continuous(name){
    let repeat = 0;
    for(let i = 0; i < name.length; i++){
        if(name[i] != "A") break;
        repeat++;
    }
    return repeat;
}
```





* 구명보트
+ https://programmers.co.kr/learn/courses/30/lessons/42885?language=javascript


```javascript
// 내소스 
function solution(people, limit) {
    var answer = 0;
    people.sort((a,b) => { return b-a; } );
    for(var i=0,r=people.length-1;i<people.length;i++) {        
        if(i > r) break;
        if(people[i]+people[r] <= limit) {
            r--;
        }
        answer++;        
    }
    return answer;
}
```


* 숫자의 표현
+ https://programmers.co.kr/learn/courses/30/lessons/12924?language=javascript


```javascript
// 내소스 
function solution(n) {
    var answer = 1;
    for(var i=1;i<n;i++) {
        let sum=i;
        for(var j=i+1;j<n;j++) {
            sum+=j;
            if(sum==n) { 
                answer++;
                break;
            }
            else if(sum>n) break;
        }
    }
    return answer;
}
```




* 행렬의 곱셈
+ https://programmers.co.kr/learn/courses/30/lessons/12949?language=javascript#


```javascript
// 내소스 
function solution(arr1, arr2) {
    return arr1.map((row) => arr2[0].map((x,y) => row.reduce((a,b,c) => a + b * arr2[c][y], 0)))

    var answer = [];    
    arr1.forEach( (d,i) => {        
        for(let j=0;j<arr2[0].length;j++) {
            let sum=0;
            for(let k=0;k<d.length;k++) {
                sum += (d[k]*arr2[k][j]);
            }
            if(!answer[i]) answer[i] = [];
            answer[i][j] = sum;
        }        
    });
    return answer;
}
```



   
***
***
   


* 가장 큰 정사각형 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/12905?language=javascript


```javascript
function solution(board)
{
    var answer = 0;
    var y = board.length;
    var x = board[0].length;
    
    // 표가 x나 y의 길이가 1일경우 가장큰값을 구한다.
    if(x<2 || y<2) {
        return Math.max([...board]);
    }
    
    for(let i=1;i<y;i++) {
        for(let j=1;j<x;j++) {
            if(board[i][j] == 1) {
                // 현재위치의 값이 1인경우
                // 왼쪽,위,왼쪽위의 3값중 가장 작은값 + 1 을 저장한다.
                let d = Math.min(board[i-1][j],board[i][j-1],board[i-1][j-1]); 
                board[i][j] = d+1;
                answer = Math.max(d+1, answer);
            }
        }
    }
    
    return answer*answer;
}
```



* 오픈채팅방
+ https://programmers.co.kr/learn/courses/30/lessons/42888?language=javascript


```javascript
// 내소스
function solution(record) {
    var answer = [];
    var user = [];
    record.forEach( (d) => {
        let arr = d.split(" ");
        if(!user[arr[1]]) user[arr[1]]=arr[2];
        // 채팅방을 나간후 다른이름으로 변경후 입장할수있기때문에, Enter도 포함하였다.
        if(arr[0] === "Change" || arr[0] === "Enter") {
            user[arr[1]]=arr[2]; 
        }
    });
    
    record.forEach( (d) => {
        let arr = d.split(" ");
        if(arr[0] == "Enter") {
            answer.push(user[arr[1]]+"님이 들어왔습니다.")            
        } else if(arr[0] == "Leave") {
            answer.push(user[arr[1]] + "님이 나갔습니다.")             
        }   
    });    
    return answer;
}
```


```javascript
// 내소스, 2022-02-06
function solution(record) {
    const ENTER = 1;
    const LEAVE = 2;
    const ENTER_STR = "님이 들어왔습니다.";
    const LEAVE_STR = "님이 나갔습니다.";
    
    var answer = [];
    var ulist = [];
    var chat = [];
    let cmd,uid,name;
    record.forEach( (d) => {
        [cmd,uid,name] = d.split(" ");
        if(cmd.localeCompare("Enter") == 0) {
            ulist[uid] = name;
            chat.push([uid,ENTER]);
        } 
        else if(cmd.localeCompare("Leave") == 0) {
            chat.push([uid,LEAVE]);
        }
        else {
            ulist[uid] = name;
        }
    });
    
    chat.forEach( (d) => {
        answer.push(ulist[d[0]] + (d[1]==ENTER?ENTER_STR:LEAVE_STR));
    });
    
    return answer;
}
```


* 타겟 넘버
+ https://programmers.co.kr/learn/courses/30/lessons/43165?language=javascript


```javascript
// 내소스
function solution(numbers, target) {
    var answer = 0;
    var arr = Array(numbers.length).fill(0);
    // 재귀호출을 사용하여 모든경우의 수를 구하여 계산하였다.
    function rcall(n) {
        if(n>=numbers.length) {
            let sum=0;
            for(let i=0;i<n;i++) 
                sum += (arr[i]*numbers[i]);
            if(sum == target) answer++;
            return;
        }
        arr[n] = -1;
        rcall(n+1);
        arr[n] = 1;
        rcall(n+1);
    }
    
    rcall(0);
    
    return answer;
}
```

```javascript
// 내소스, 2022-02-21
function solution(numbers, target) {
    var answer = 0;
    
    function recursive(idx) {
        if(idx >= numbers.length) {
            if( target == numbers.reduce((a,d) => a+d)) answer++;
            return;
        }
        recursive(idx+1);
        numbers[idx] *= -1;
        recursive(idx+1);        
    }
    
    recursive(0);    
    return answer;
}
```


* 땅따먹기
+ https://programmers.co.kr/learn/courses/30/lessons/12913?language=javascript


```javascript
// 남의소스
function solution(land) {
    var answer = 0;
    for(let i=1;i<land.length;i++) {
        land[i][0] += Math.max(land[i-1][1],land[i-1][2],land[i-1][3]);
        land[i][1] += Math.max(land[i-1][0],land[i-1][2],land[i-1][3]);
        land[i][2] += Math.max(land[i-1][0],land[i-1][1],land[i-1][3]);
        land[i][3] += Math.max(land[i-1][0],land[i-1][1],land[i-1][2]);        
    }
    answer = Math.max(...land[land.length-1]);
    return answer;
}
```


   
***
***
   

* 스킬트리
+ https://programmers.co.kr/learn/courses/30/lessons/49993?language=javascript


```javascript
// 내소스
function solution(skill, skill_trees) {
    var answer = 0;
    var arr=[...skill];
    skill_trees.forEach( (d) => {
        let str = "";
        [...d].forEach( (d2) => { if(arr.indexOf(d2) >=0) str += d2; });
        if(skill.indexOf(str) == 0) answer++; 
    });
    return answer;
}
```

function solution(skill, skill_trees) {
    function isCorrect(n) {
        // const test = '[' + 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').filter(v => !skill.includes(v)).join('') + ']*';
        let test = skill.split('');
        for (var i = 0; i < n.length; i++) {
            if (!skill.includes(n[i])) continue;
            if (n[i] === test.shift()) continue;
            return false;
        }
        return true;
    }    

    return skill_trees.filter(isCorrect).length;
}


* 멀쩡한 사각형
+ https://programmers.co.kr/learn/courses/30/lessons/62048?language=javascript


```javascript
// 
function solution(w, h) {
    function gcd(w,h) {
        let mod = w%h;
        if(mod==0) return h;
        return gcd(h,mod);
    }

    return w*h - (w+h-gcd(w,h));
}
```



* 문자열 압축
+ https://programmers.co.kr/learn/courses/30/lessons/60057?language=javascript


```javascript
// 
function solution(s) {
    var answer = 0;
    var repeat = Math.floor(s.length / 2);
    var arrForNewStr = [];
    
    // 문자열의 길이가 1이면 그냥 1리턴
    if(s.length==1) return 1;
    
    for (var i=0; i<repeat; i++) {
        var num = i+1; // 압축 기준 단위 수
        var count = 1; // 동일 글자가 몇 번 반복되는지
        var newStr = '';
        for (var j=0; j<s.length; j=j+num) { // 하나의 단위에 대한 
            var currentSub = s.substring(j, j+num); //substring(a,b)
            var nextSub = s.substring(j+num, j+num+num);
      
            if( currentSub === nextSub) {   // 이전문자열과 같으면 1 증가 
                count += 1;
            } else {    // 문자열이 다르면 
                if(count !== 1){    // 동일한문자열이 2이상일경우
                     newStr = newStr + count + currentSub;
                } else {    // 압축이 안되는 문자열이므로, 그냥 붙인다. 
                     newStr = newStr + currentSub;
                } 
                count = 1;
            }
        
        }  
        
        // 2. 각 경우의 문자열 개수중 가장 짧은 것
        arrForNewStr.push(newStr.length);
    }
    
    
    answer = Math.min(...arrForNewStr);
   
    
    return answer;
}
```


```javascript
// 2022-02-06
function solution(s) {
    var answer = s.length;
    let mid = parseInt(s.length/2);
    for(let i=1;i<=mid;i++) {
        let dup = 1;
        let one = "";
        let cnt = 0;
        for(let j=0;j<s.length;j++) {
            let two = s.substr(i*j,i);
            if(two.length < i) break;
            if(one.localeCompare(two) == 0) {
                dup++;
            }
            else {
                if(dup>1) {
                    cnt = cnt + (i*dup - (dup+one).length);
                }
                one = two;
                dup=1;
            }
        }
        
        if(dup>1) {
            cnt = cnt + (i*dup - (dup+one).length);
        }        
        answer = Math.min(answer,s.length-cnt);
    }

    return answer;
}
```



* 괄호 변환
+ https://programmers.co.kr/learn/courses/30/lessons/60058?language=javascript


```javascript
// 내소스
function solution(p) {
    var answer = '';
    
    function split(p) {
        let left=0,right=0;
        for(let i=0;i<p.length;i++) {
            if(p[i] == "(") left++;
            if(p[i] == ")") right++;
            if(left == right) {
                return  { u:p.substr(0,i+1), v:p.substr(i+1) };
            }
        }
        return { u:p, v:"" };
    }

    function reverse(p) {
    	let str = "";
        for(let i=1;i<p.length-1;i++) {
            if(p[i] === "(") 
            	str+=")";
            else
            	str+="(";
        }
        return str;
    }

    function process(p) {
        if (p.length < 1) return "";
        let {u, v} = split(p);
        if(u[0]=="(" && u[u.length-1] ==")") return u + process(v);
        else {
            return "(" + process(v) + ")" + reverse(u);
        }        
    }
    answer = process(p);
    
    return answer;
}
```


```javascript
// 다른사람소스
function reverse(str) {
  return str.slice(1, str.length - 1).split("").map((c) => (c === "(" ? ")" : "(")).join("");
}

function solution(p) {
  if (p.length < 1) return "";

  let balance = 0;
  let pivot = 0;
  do { balance += p[pivot++] === "(" ? 1 : -1 } while (balance !== 0);

  const u = p.slice(0, pivot);
  const v = solution(p.slice(pivot, p.length));

  if (u[0] === "(" && u[u.length - 1] == ")") return u + v;
  else return "(" + v + ")" + reverse(u);
}
```

   
***
***
   




* 튜플
+ https://programmers.co.kr/learn/courses/30/lessons/64065?language=javascript


```javascript
// 내소스
function solution(s) {
    var answer = [];
    
    var arr = [];
    var str = "";
    [...s.substr(1,s.length-2)].forEach( (d) => {
        if(d == "{") 
            str = "";
        else if(d == "}") 
            arr.push(str);
        else 
            str += d;
    });
    arr.sort( (a,b) => {return a.length-b.length;});
    
    arr.forEach( (d) => {
        d.split(",").map( (item) => parseInt(item)).forEach( (d2) => {            
            if( answer.indexOf(d2) == -1)  answer.push(parseInt(d2));
        });
    });
    
    return answer;
}
```

```javascript
// 개선된 내소스
    s.substr(2,s.length-4).split('},{').sort( (a,b) => {return a.length-b.length;}).map(v => v.split(',').map(v => +v)).forEach( (d) => {
        d.forEach( d2 => {
            if( answer.indexOf(d2) == -1)  answer.push(d2);
        })
    });   

    // s="{{1,2,3},{2,1},{1,2,4,3},{2}}"; ==> "1,2,3", "2,1",....이렇게 문자열을 나눠서 배열에 넣는다.
    // s.substr(2,s.length-4).split('},{') 

    // 문자열을 길이가 짧은순으로 정렬한다.
    // sort( (a,b) => {return a.length-b.length;})

    // 각각의 배열을 map을 사용하여, 다시 ","을 기준으로 문자열을 배열로 만든다. v=>+v로 문자를 순자로 변환한다.
    // "1,2,3" ==> [1,2,3] 으로 변환됨
    // map(v => v.split(',').map(v => +v))

    // [[2] , [2,1], [1,2,3], [1,2,4,3]] 이렇게 2차원 배열로 되어 있어서, 
    // 아래와 같이 forEach를 사용하여, answer배열에 없으면 push한다.
    // forEach( (d) => {
    //    d.forEach( d2 => {
    //        if( answer.indexOf(d2) == -1)  answer.push(d2);
    //    })
    // });   
```


* 폰켓몬
+ https://programmers.co.kr/learn/courses/30/lessons/1845?language=javascript


```javascript
// 내소스
function solution(nums) {
    var answer = 0;
    var cnt = parseInt(nums.length/2);
    var set = new Set(nums);
    if(cnt<set.size) answer=cnt;
    else answer = set.size;
    return answer;
}
```


* 이진 변환 반복하기
+ https://programmers.co.kr/learn/courses/30/lessons/70129?language=javascript


```javascript
// 내소스
function solution(s) {
    var answer = [];
    var zero=0;
    
    function rec(s,fcnt=0) {
        if(s == "1")
            return 0;
        let cnt=0;
        for(let i=0;i<s.length;i++)
            if(s.charAt(i) == 0)
                cnt++;
        zero += cnt;
        
        return rec((s.length-cnt).toString(2)) + 1;
    }
    
    answer.push(rec(s));
    answer.push(zero);
    
    return answer;
}
```


* 짝지어 제거하기
+ https://programmers.co.kr/learn/courses/30/lessons/12973?language=javascript


```javascript
// 내소스
function solution(s)
{
    let stack=[];
    for(let i=0;i<s.length;i++) {
        if(stack[stack.length-1] == s.charAt(i)) stack.pop();
        else stack.push(s.charAt(i));
    }
    return stack.length==0?1:0;
}
```



   
***
***
      



* 쿼드압축 후 개수 세기
+ https://programmers.co.kr/learn/courses/30/lessons/68936?language=javascript


```javascript
// 내소스
function solution(arr) {
    var answer = [0,0];
    
    function rec(x,y,x2,y2) {
        if(x2-x == 1) {
            let ar = [ 0,0 ];
            ar[arr[x][y]]++;
            ar[arr[x][y2]]++;
            ar[arr[x2][y]]++;
            ar[arr[x2][y2]]++;
            if(ar[0] == 4) return 0;
            if(ar[1] == 4) return 1;
            answer[0] += ar[0];
            answer[1] += ar[1];
            return -1;
        }
        else {
            let sz = Math.floor((x2-x)/2);
            let set = new Set();
            let ar = [ 0,0 ];
            ar[rec(x,y,x+sz,y+sz)]++;
            ar[rec(x+sz+1,y,x2,y+sz)]++;
            ar[rec(x,y+sz+1,x+sz,y2)]++;
            ar[rec(x+sz+1,y+sz+1,x2,y2)]++;
            if(ar[0] == 4) return 0;
            if(ar[1] == 4) return 1;
            answer[0] += ar[0];
            answer[1] += ar[1];
            return -1;
        }
    }
    
    let ret = rec(0,0,arr.length-1,arr.length-1);
    if(ret>=0) answer[ret]++;
    
    return answer;
}
```



* 삼각 달팽이
+ https://programmers.co.kr/learn/courses/30/lessons/68645?language=javascript


```javascript
// 내소스
function solution(n) {
    var answer = [];
    
    var arr = Array.from(Array(n), () => Array());
    console.log(arr);
    
    let cnt = 1;
    let x=0,y=-1;    
    for(;;) {
        for(let i=0;i<n;i++) {
            arr[++y][x] = cnt++;
        }
        n--;
        if(n===0) break;
        for(let i=0;i<n;i++) {
            arr[y][++x] = cnt++;
        }
        n--;
        if(n===0) break;
        for(let i=0;i<n;i++) {
            arr[--y][--x] = cnt++;
        }
        n--;
        if(n===0) break;
    }
    
    arr.forEach( (d) => { d.forEach( (d2) => answer.push(d2) ) } );
    return answer;
}
```


```javascript
// 내소스(좀더 간결하게정리함.)
function solution(n) {
    var answer = [];
    
    var arr = Array.from(Array(n), () => Array());
    console.log(arr);
    
    let x=0,y=-1;    
    for(let k=n,cnt=1;k>0;k-=3) {
        for(let i=0;i<k;i++) arr[++y][x] = cnt++;
        for(let i=0;i<k-1;i++) arr[y][++x] = cnt++;
        for(let i=0;i<k-2;i++) arr[--y][--x] = cnt++;
    }
    
    arr.forEach( (d) => { d.forEach( (d2) => answer.push(d2) ) } );
    return answer;
}
```



* 영어 끝말잇기
+ https://programmers.co.kr/learn/courses/30/lessons/12981?language=javascript


```javascript
// 내소스
function solution(n, words) {
    let set = new Set();
    let i=0;
    let ch = words[0].charAt(0);
    for(;i<words.length;i++) {
        if(ch !== words[i].charAt(0) || set.has(words[i]) == true) 
            break;
        set.add(words[i]);
        ch = words[i].charAt(words[i].length-1);
    }
    
    if(i==words.length) return [0,0];
    return [ i%n+1,Math.floor(i/n)+1  ] ;
}
```


* 점프와 순간 이동
+ https://programmers.co.kr/learn/courses/30/lessons/12980?language=javascript


```javascript
// 내소스
function solution(n)
{
    var ans = 0;

    function rec(n) {        
        if(n==1) return 1;
        if(n%2 == 0) 
            return rec(n/2);
        return 1+rec((n-1)/2);
    }    
    ans = rec(n);

    return ans;
}
```



   
***
***
      





* [카카오 인턴] 수식 최대화
+ https://programmers.co.kr/learn/courses/30/lessons/67257?language=javascript


```javascript
// 남의소스
function solution(expression) {
    const prior = [
        ['-', '*', '+'],
        ['-', '+', '*'],
        ['*', '-', '+'],
        ['*', '+', '-'],
        ['+', '-', '*'],
        ['+', '*', '-']
    ]
    let cand = []

    // 수식을 배열로 분리하여 저장한다. 
    // "100-200*300-500+20" => [ '100', '-', '200', '*', '300', '-', '500', '+', '20' ]
    const arr = expression.split(/(\D)/)
    prior.forEach( (opCand) => {
        // arr배열을 복사하여 temp에 넣는다.
    	const temp = arr.slice();
    	opCand.forEach( (exp) => {
            // includes : 배열이 특정요소를 포함하는지 판별한다.
            while (temp.includes(exp)) {
                const idx = temp.indexOf(exp);
                // idx : 현재 연산자의 위치 
                // temp.splice(idx - 1, 3, ???) => 현재 연산자의 앞,뒤 숫자를 연산해야하기때문에, -1부터 3개의 요소를 추출하여, 배열에서 제거한다. 그후 ???를 넣는다.
                // eval() : 문자열을 연산하는 함수 : evel("2_2"); ==> 결과값은 4 가 나온다.
                // temp.slice(idx - 1, idx + 2).join('') => temp배열의 idx-1 부터 idx+2가지를 추출하여 문자열로 만든다.
                temp.splice(idx - 1, 3, eval(temp.slice(idx - 1, idx + 2).join('')));
            }
        });
        cand.push(Math.abs(temp[0]))
    });
    return Math.max(...cand)
}
```



* JadenCase 문자열 만들기
+ https://programmers.co.kr/learn/courses/30/lessons/12951?language=javascript


```javascript
// 내소스
function solution(s) {
    return s.split(" ").map( (d)=>{
        return (d ==='')?'' : d[0].toUpperCase() + d.substr(1).toLowerCase();
    }).join(" ");
}
```


* N개의 최소공배수
+ https://programmers.co.kr/learn/courses/30/lessons/12953?language=javascript


```javascript
// 내소스
function solution(arr) {    
    function gcdFunc(a,b) {
        while(b>0) {
            let tmp = b;
            b = a%b;
            a = tmp;
        }
        return a;
    }
    
    var answer = arr[0];
    for(let i=1;i<arr.length;i++) {
        answer = answer*arr[i]/gcdFunc(answer,arr[i]);       
    }
    
    return answer;
}
```
// 다른사람 소스
function solution(arr) {
    function gcd(a,b) { return a%b?gcd(b,a%b):b }
    return arr.reduce((a,b)=> a*b/gcd(a,b));
}

* 예상 대진표
+ https://programmers.co.kr/learn/courses/30/lessons/12985?language=javascript#


```javascript
// 다른사람소스
function solution(n,a,b)
{
    var answer = 0;

    while(a!=b) {
        a = Math.ceil(a/2);
        b = Math.ceil(b/2);
        answer++;
    }

    return answer;
}
```



   
***
***
      



* [1차] 뉴스 클러스터링
+ https://programmers.co.kr/learn/courses/30/lessons/17677?language=javascript


```javascript
// 내소스
function solution(str1, str2) {
    function convertArr(str) {
        var arr= [];
        [...str.toUpperCase()].reduce( (a,b) => { 
            if(a.toLowerCase() != a && b.toLowerCase() != b)
                arr.push(a+b);
            return b; 
        });
        return arr.sort();   
    }
    
    var arr1 = convertArr(str1);
    var arr2 = convertArr(str2);
    let i1=0;
    let i2=0;
    var inter = []; // 교집합
    var union = []; // 합집합
    for(;;) {
        // 어느 한쪽의 배열이 끝이라면 나머지 배열을 합집합에 넣는다.
        if(arr1.length <= i1) {
            for(let i=i2;i<arr2.length;i++) union.push(arr2[i2]);
            break;
        }
        if(arr2.length <= i2) {
            for(let i=i1;i<arr1.length;i++) union.push(arr1[i1]);
            break;
        }
        
        let a = arr1[i1];
        let b = arr2[i2];
        if(a == b) {
            inter.push(a);
            union.push(a);
            i1++;
            i2++;
        }
        else if(a>b) {
            union.push(b);
            i2++;
        }
        else if(a<b) {
            union.push(a);
            i1++;
        }         
    }
    if(inter.length == 0 && union.length == 0) return 65536;
    return Math.floor(inter.length/union.length*65536);
}
```

```javascript
// 다른사람소스
function solution(str1, str2) {
    var answer = 0;
    // 일단 대문자로 모두 변환한다.
    str1 = str1.toUpperCase();
    str2 = str2.toUpperCase();
    // 정규식을 사용하여 문자만 추출한다.
    var st1A = Array.apply(null, Array(str1.length-1)).map((a,i)=>str1[i]+str1[i+1]).filter(a=>/^[a-zA-Z]+$/.test(a));
    var st2A = Array.apply(null, Array(str2.length-1)).map((a,i)=>str2[i]+str2[i+1]).filter(a=>/^[a-zA-Z]+$/.test(a));
    var co = 0;
    st1A.map(a=>{
        var i = st2A.indexOf(a);
        if (i>-1) {
            co++;
            st2A.splice(i,1);
        }
    });
    var mo = st1A.length + st2A.length;

    if (mo ===0) {
        return 65536;
    } else {
        return Math.floor(65536 * co / mo);
    }
}
```


* [1차] 캐시
+ https://programmers.co.kr/learn/courses/30/lessons/17680?language=javascript


```javascript
// 내소스
function solution(cacheSize, cities) {
    var answer = 0;
    // 모두 대문자로 변환
    cities = cities.map( (d) => { return d.toUpperCase(); });
    var cache = [];
    
    // 캐시 사이즈가 0이면 5를 곱해서 리턴
    if(cacheSize==0) return cities.length*5;
    
    cities.forEach( (d) => {
        let idx = cache.indexOf(d);
        if(idx === -1) {
            // 캐시에 없으면 5의 비용을 소모
            answer+=5;
            // 캐시가 다 찼으면 맨앞을 삭제
            if(cache.length >= cacheSize) cache.shift();
        }
        else {
            // 캐시에 있으면 1의 비용을 소모
            answer++;
            // 해당 데이타를 삭제
            cache.splice(idx,1);
        } 
        // 캐시에 추가
        cache.push(d);
    });
    
    return answer;
}
```


* [3차] 파일명 정렬
+ https://programmers.co.kr/learn/courses/30/lessons/17686?language=javascript


```javascript
// 남의소스
function solution(files) {
    var answer = [];
    // 
    let answerWrap = files.map((file, index) => ({file, index}));
 
    var compare = (a,b)=>{
        var regexNum = /[0-9]/g;
        var numIndexA = a.indexOf((a.match(regexNum))[0]);
        var numIndexB = b.indexOf((b.match(regexNum))[0]);
        // a,b 의 Head부분의 문자열을 비교한다.
        var sortByHead = (a.substring(0, numIndexA)).toLowerCase().localeCompare(b.substring(0, numIndexB).toLowerCase());

        //1, -1, 0
        if(sortByHead === 0) {// Num기준 정렬
            var subStrA = parseInt(a.substring(numIndexA));
            var subStrB = parseInt(b.substring(numIndexB));
            if(subStrA<subStrB){
                return -1;
            }else if(subStrA>subStrB){
                return 1;
             }else {
               return 0;
            }
         } else 
             return sortByHead;;
     }

   answerWrap.sort((a, b) => {
      var result = compare(a.file, b.file);
      // 두 Head값도 같고, 숫자도 같을 경우 index를 기준으로 오름차순 정렬한다.
      return result === 0 ? a.index - b.index : result;
    })
    return answerWrap.map(answer => answer.file);
}
```


* [1차] 프렌즈4블록
+ https://programmers.co.kr/learn/courses/30/lessons/17679?language=javascript


```javascript
// 남의소스
function solution(m, n, board) {
    board = board.map(v => v.split(''));

    while (true) {
        let founded = [];

        // 찾기 - 네 개중 우측 하단 모서리 인덱스 기준
        for (let i = 1; i < m; i++) {
            for (let j = 1; j < n; j++) {
                if (board[i][j] && board[i][j] === board[i][j - 1] && board[i][j] === board[i - 1][j - 1] && board[i][j] === board[i - 1][j]) {
                    founded.push([i, j]);
                }
            }
        }

        if (! founded.length) 
          return [].concat(...board).filter(v => ! v).length;

        // 부수기 - 지워질 것 0으로 채우기
        founded.forEach(a => {
            board[a[0]][a[1]] = 0;
            board[a[0]][a[1] - 1] = 0;
            board[a[0] - 1][a[1] - 1] = 0;
            board[a[0] - 1][a[1]] = 0;
        });

        // 재정렬 - ?? 이부분 이해가 안돼..
        for (let i = m - 1; i > 0; i--) {
            if (! board[i].some(v => ! v)) continue;

            for (let j = 0; j < n; j++) {
                for (let k = i - 1; k >= 0 && ! board[i][j]; k--) {
                    if (board[k][j]) {
                        board[i][j] = board[k][j];
                        board[k][j] = 0;
                        break;
                    }
                }
            }
        }
    }
}
```



   
***
***
      




* 후보키
+ https://programmers.co.kr/learn/courses/30/lessons/42890?language=javascript


```javascript
// 남의소스
function solution(relation) {
    const cols = relation[0].length
    const rows = relation.length
    // 4가지의 키라면, 1<<4번 shift하기때문에 16이 나옴. 1~15
    const sets = 1 << cols
    const sk = new Set()

	// 키가 4라면 1~15까지 
    for (let i=1; i<sets; i++) {
        const tmp = new Set()
        // row : 레코드 갯수 
        for (let row=0; row<rows; row++) {
            let key = ''
            // cols : 컬럼 갯수
            for (let col=0; col<cols; col++) {
            	// 0001 ~ 1111 중 조건에 만족하면 키를 만든다. 
                if (i & (1 << col)) key = String(key) + String(relation[row][col])
            }
            tmp.add(key)
        }
        // Set이기 때문에 총갯수가 같으면 sk에 add한다. 
        if (tmp.size === rows) sk.add(i)
    }

	// set을 순회한다.
    for (let i of sk) {
        for (let j of sk) {
        	// i는 무조건 j보다 커야한다.
            if (i >= j) continue;
            // i&j and연상이 i와 같으면 j를 삭제한다. 
            if ((i & j) === i) sk.delete(j)
        }
    }

	// 어떤키가 유니크인지 출력한다. 
    // console.log(Array.from(sk).map(e => e.toString(2)))

    return sk.size
}
```


```javascript
// 다른소스
function solution(relation) {
    const cols = relation[0].length;

    const check = 1 << cols;
    const answer = new Set();

    for(let i = 1; i < check; i++){

        // relation.map( function(x) { console.log(x); }); // x는 [ 100,"abc","kim"] 같은 배열임
        // x.filter((col,index)=>i & (1<<index)).join("") ==> col (Data) , idx(0,1,2같은 값들.)
        let temp = relation.map(x=>x.filter((col,index)=>i & (1<<index)).join(""));
        const set  = new Set(temp);

        if(temp.length === set.size) answer.add(i);
    }

    for( let x of answer){
        for ( let y of answer){
            if(x >= y) continue;
            if((x & y) === x) answer.delete(y);
        }
    }

	console.log(answer);
    return answer.size;
}
```


* [3차] 방금그곡
+ https://programmers.co.kr/learn/courses/30/lessons/17683?language=javascript


```javascript
// 남의소스
function solution(m, musicinfos) {
    // [문자+#] 인 항목을 찾아서 소문자로 변환한다. 
    // ex) CC#BCC#BCC#BCC#B ==> CcBCcBCcBCcB
   const _m = m.replace(/(\D)#/g, (s,p1)=>p1.toLowerCase());
   

    const broadcast = musicinfos.map(x=>{
        // ,를 기준으로 시작시간,끝시간,제목,악보를 분리한다. ex) "03:00,03:30,FOO,CC#B" ==> [ '03:00', '03:30', 'FOO', 'CC#B' ]
        const info = x.split(",");
        // 악보를 [문자+#] 인 항목을 찾아서 소문자로 변환한다. 
        const song = info[3].replace(/(\D)#/g, (s,p1)=>p1.toLowerCase());
        // 음악제목, 
        return [info[2],play(toMinute(info[1].split(":"))- toMinute(info[0].split(":")), song)];
    });
    const answer = broadcast.reduce((answer, x)=>{
        // 악보에 _m이 포함되어 있으면,
        if(x[1].includes(_m)){
            // answer (0:이름 1:악보 인 배열) 보다 더 긴 악보라면 x로 교체한다. 
            if(answer.length == 0|| answer[1].length < x[1].length) return x;
        }
        return answer;
    },[]);
    console.log(answer);
    return (answer.length == 0)? "(None)" : answer[0];
}

// 시간계산 
function toMinute(t){
    return (t[0]*60) + (t[1]*1);
}

// song을 time만큼 늘린다. 
// ex) 30 , 'CcB' => CcBCcBCcBCcBCcBCcBCcBCcBCcBCcB
// ex) 8, 'CcBCcBCcB' => CcBCcBCc
function play(time, song){
    const length = song.length;
    return song.repeat(time / length) + song.substring(0, time % length);
}
```


* N진수 게임
+ https://programmers.co.kr/learn/courses/30/lessons/17687?language=javascript


```javascript
// 남의소스
// 진법 n, 미리 구할 숫자의 갯수 t, 게임에 참가하는 인원 m, 튜브의 순서 p
function solution(n, t, m, p) {
  const answer = [];
  let tmp = [];
  let i = 1;
  let num = 0;
  while (answer.length !== t) {
    // tmp가 비어 있으면 num을 string으로 변환한다. 
    if (!tmp.length) {
      tmp = num.toString(n).split('');
      num++;
    }
    // tmp에서 값을 1개 갖고 온다. ("12" => "1")
    const nowNum = tmp.shift();
    // 튜브의 순서라면 push한다. 
    if (i === p) answer.push(nowNum);
    i++;
    // i가 인원보다 크면 1로 수정한다. 
    if (i > m) i = 1;
  }
  return answer.map((v) => v.toUpperCase()).join('');
}

// console.log(solution(16,16,4,1));
```


* [1차] 추석 트래픽
+ https://programmers.co.kr/learn/courses/30/lessons/17676


```javascript
// 남의소스
const solution = (lines) => {
  let answer = 0;
  const arr = [];
  const logPointArr = [];

  //1. 로그데이터를 나누고 시작초와 끝초를 새로운 배열에 담는다.
  for (let i = 0; i < lines.length; i++) {
    const line = lines[i].split(" ");
    const edSec =
      Number(line[1].substring(0, 2)) * 3600 +
      Number(line[1].substring(3, 5)) * 60 +
      Number(line[1].substring(6, 12));
      
    const duration = Number(line[2].substring(0, line[2].length - 1));
    
    const stSec = edSec - duration + 0.001;

    arr.push([stSec, edSec]);
    logPointArr.push(stSec, edSec);
  }
  
  //시작초와 끝초를 정렬한다 순서대로 순회하기 위해서..
  logPointArr.sort();
  // arr : 시작,끝시간이 저장된 2차원 배열 
  // logPointArr : 시작,끝시간정보만 저장된 1차원배열


  for (let i = 0; i < logPointArr.length; i++) {
  	// beginRange~endRange는 1초 , 서버의 처리시간이 1초이므로 
    const beginRange = logPointArr[i];
    const endRange = logPointArr[i] + 1;

    let count = 0;
    for (let j = 0; j < arr.length; j++) {
      const stPoint = arr[j][0];
      const edPoint = arr[j][1];

      //위 경우는 세가지로 나눌 수 있다 : 1. 시작점이 범위에 포함될때, 2.끝점이 범위에 포함될때,
      //3.시작점과 끝점사이가 범위에 포함될때
      if (
        (stPoint >= beginRange && stPoint < endRange) ||
        (edPoint >= beginRange && edPoint < endRange) ||
        (stPoint <= beginRange && edPoint >= endRange)
      ) {
        count++;
      }
    }

    // count : 1초동안에 처리된 작업수

    if (count > answer) {
      answer = count;
    }
  }
  return answer;
};

```



   
***
***
      




* 행렬 테두리 회전하기
+ https://programmers.co.kr/learn/courses/30/lessons/77485

 
```javascript
// 내소스 2021.12.24
function solution(rows, columns, queries) {
    var answer = [];
    var arr = [];
    for(let i=0;i<rows*columns;i++) {
        // console.log(i + ":" + parseInt(i/columns) + ":"+i%columns);
        let x = parseInt(i/columns);
        let y = i%columns;
        if(y==0) arr[x] = [];
        arr[x][y] = i+1;
    }
    
    queries.forEach( (d) => {
        let y1 = d[0]-1;  // 5
        let x1 = d[1]-1;  // 1
        let y2 = d[2]-1;  // 6
        let x2 = d[3]-1;  // 3 
  
        
        let i,tmp;
        let prev = arr[y1][x1];
        let min = prev;
        for(i=x1+1;i<=x2;i++) {
            tmp = arr[y1][i];
            arr[y1][i] = prev;
            min = Math.min(min,prev);
            prev =tmp;
        }
        for(i=y1+1;i<=y2;i++) {
            tmp = arr[i][x2];
            arr[i][x2] = prev;
            min = Math.min(min,prev);
            prev =tmp;           
        }
        for(i=x2-1;i>=x1;i--) {
            tmp = arr[y2][i];
            arr[y2][i] = prev;            
            min = Math.min(min,prev);
            prev =tmp;
        }
        for(i=y2-1;i>=y1;i--) {
            tmp = arr[i][x1];
            arr[i][x1] = prev;
            min = Math.min(min,prev);
            prev =tmp
        }
        
        answer.push(min);
        
    });

    return answer;
}
```



* 
+ 

* n^2 배열 자르기
+ https://programmers.co.kr/learn/courses/30/lessons/87390?language=javascript
```javascript
// 내소스
function solution(n, left, right) {
    var answer = [];
    var arr = [];
    var idx = 0;
    for(let x=1;x<=n;x++) {
        if(idx>right) break;
        if(idx+n < left) {
            idx += n;
            continue;
        }
        for(let y=1;y<=n;y++) {
            let d = y<=x?x:y;            
            if(idx>=left && idx<=right) answer.push(d);
            idx++;
        }
    }
    return answer;
}
```

```javascript
// 내소스(개선됨)
function solution(n, left, right) {
    var answer = [];
    var arr = [];
    var idx = 0;
    let x = parseInt(left/n)+1;
    idx = n * (x-1);
    
    for(;x<=n;x++) {
        if(idx>right) break;
        if(idx+n < left) {
            idx += n;
            continue;
        }

        for(let y=1;y<=n;y++) {
            let d = y<=x?x:y;            
            if(idx>=left && idx<=right) answer.push(d);
            idx++;
        }
    }
    return answer;
}
```

* 
+ 


```javascript
// 내소스

```


* 
+ 


```javascript
// 내소스

```



   
***
***
      

