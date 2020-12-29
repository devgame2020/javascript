# 프로그래머스 코딩 테스트


* 가운데 글자 가져오기 : <https://programmers.co.kr/learn/courses/30/lessons/12903>
   
+ 내소스
```
function solution(s) {
    var answer = '';
    var r = parseInt(s.length)%2;
    var mid = parseInt(s.length/2);   
    if(r) answer = s.substring(mid,mid+1);
    else answer = s.substring(mid-1,mid+1);
    return answer;
}
```

+ 다른 사람소스
+ Math.ceil() : 올림함수 
    + Math.ceil(s.length / 2) - 1
        + abc ==> 1 
        + abcd ==> 1
        + abcde ==> 2
    + s.length % 2 === 0 ? 2 : 1
        + 짝수면 2 , 홀수면 1
```
function solution(s) {
    return s.substr(Math.ceil(s.length / 2) - 1, s.length % 2 === 0 ? 2 : 1);
}
```
   
***
   
* 크레인 인형뽑기 게임 : <https://programmers.co.kr/learn/courses/30/lessons/64061>
   

+ 내소스
```
function solution(board, moves) {
    var answer = 0;
    var len = board.length;
    var arr = Array();
    // moves의 모든 배열을 순환한다. 
    moves.forEach(function(item) {
        item--;
        for(var i=0;i<len;i++) {
            if(board[i][item] != 0) {
                if(arr.length && arr[arr.length-1] == board[i][item]) {
                    arr.pop();
                    answer += 2;
                }
                else 
                    arr.push(board[i][item]);
                board[i][item] = 0;
                break;
            }
        }
    });
  
    return answer;
}
```

+ 다른 사람 소스 
```
const transpose = matrix =>
    matrix.reduce(
        (result, row) => row.map((_, i) => [...(result[i] || []), row[i]]),
        []
    );

const solution = (board, moves) => {
    const stacks = transpose(board).map(row =>
        row.reverse().filter(el => el !== 0)
    );
    const basket = [];
    let result = 0;

    for (const move of moves) {
        const pop = stacks[move - 1].pop();
        if (!pop) continue;
        if (pop === basket[basket.length - 1]) {
            basket.pop();
            result += 2;
            continue;
        }
        basket.push(pop);
    }

    return result;
};
```

   
***
   

* 완주하지 못한 선수 : <https://programmers.co.kr/learn/courses/30/lessons/42576>
   
+ 내소스

```
// 두배열을 merge한후에 정렬하여, 해당 배열을 순회하면서 같은 값이 홀수인 항목이 정답!
function solution(participant, completion) {
    var answer = '';
    
    var arr = participant.concat(completion);
    arr.sort();
    var cnt = 0;
    var str = "";
    arr.some(function(item) { 
        answer = item;
        if(str == item) cnt++;
        else {
            if(cnt%2 == 1) { answer = str;  return true; }
            str = item;
            cnt = 1;
        }

    });  
    return answer;
}
```

+ 다른사람소스 

```
// 두배열을 정렬하여 각각의 요소를 비교하여 서로 다를경우 해당 값이 정답!
function solution(participant, completion) {
    /*
    for(let i in participant) {
        if(completion.includes(participant[i]) == false) return participant[i];
        completion.splice(completion.indexOf(participant[i]), 1);
    }
    */

    participant.sort();
    completion.sort();

    for(let i in participant) {
        if(participant[i] !== completion[i]) return participant[i];
    }
}
```

* https://programmers.co.kr/learn/courses/30/lessons/68644

+ 두 개 뽑아서 더하기

```
// 내소스 
function solution(numbers) {
    var answer = [];
    var arr = [];
    for(let i=0;i<numbers.length-1;i++) 
        for(let j=i+1;j<numbers.length;j++) 
            arr[numbers[i]+numbers[j]] = 1;
        
    arr.forEach(function(item,idx) {
        answer.push(idx);
    });

    return answer;
}
```


```
// 수정된 소스
function solution(numbers) {
    var answer = [];
    var set = new Set();    
    for(let i=0;i<numbers.length-1;i++) 
        for(let j=i+1;j<numbers.length;j++) 
            set.add(numbers[i]+numbers[j]);
    answer = [...set].sort(function(a,b) { return a-b; });
    return answer;
}
```


```
// 다름사람 풀이
function solution(numbers) {
    const temp = []

    for (let i = 0; i < numbers.length; i++) {
        for (let j = i + 1; j < numbers.length; j++) {
            temp.push(numbers[i] + numbers[j])
        }
    }

    const answer = [...new Set(temp)]

    return answer.sort((a, b) => a - b)
}

```



   
***
***
   

* https://programmers.co.kr/learn/courses/30/lessons/42840
+ 모의고사

```
// 내소스
function solution(answers) {
    var answer = [];
    var arr = [ [], [1,2,3,4,5], [2,1,2,3,2,4,2,5] , [3,3,1,1,2,2,4,4,5,5]]; 
    var jumsu = [ 0,0,0,0 ];
    answers.forEach(function(item,idx) {
        for(let i=1;i<=3;i++) 
            if(item == arr[i][idx%arr[i].length]) 
                jumsu[i]++;            
    });

    var m = Math.max(Math.max(jumsu[1], jumsu[2]), jumsu[3]);
    for(let i=1;i<=3;i++) if(m == jumsu[i]) answer.push(i);
    answer = answer.sort(function(a,b) { return a-b; });    
    
    return answer;
}
```


```
// 수정된 소스
function solution(answers) {
    var answer = [];
    var arr = [ [], [1,2,3,4,5], [2,1,2,3,2,4,2,5] , [3,3,1,1,2,2,4,4,5,5]]; 
    var jumsu = [ 0,0,0,0 ];
    answers.forEach(function(item,idx) {
        for(let i=1;i<=3;i++) 
            if(item == arr[i][idx%arr[i].length]) 
                jumsu[i]++;            
    });

    var m = Math.max(jumsu[1], jumsu[2], jumsu[3]);
    for(let i=1;i<=3;i++) if(m == jumsu[i]) answer.push(i);
    
    return answer;
}
```

```
// 다름사람 풀이
function solution(answers) {
    var answer = [];
    var a1 = [1, 2, 3, 4, 5];
    var a2 = [2, 1, 2, 3, 2, 4, 2, 5]
    var a3 = [ 3, 3, 1, 1, 2, 2, 4, 4, 5, 5];

    var a1c = answers.filter((a,i)=> a === a1[i%a1.length]).length;
    var a2c = answers.filter((a,i)=> a === a2[i%a2.length]).length;
    var a3c = answers.filter((a,i)=> a === a3[i%a3.length]).length;
    var max = Math.max(a1c,a2c,a3c);

    if (a1c === max) {answer.push(1)};
    if (a2c === max) {answer.push(2)};
    if (a3c === max) {answer.push(3)};


    return answer;
}
```






   
***
   

* 체육복
+ https://programmers.co.kr/learn/courses/30/lessons/42862?language=javascript

```
function solution(n, lost, reserve) {
    var answer = 0;
	// 배열을 선언과 동시에 초기화하는 법. 
    var arr = Array.from({length:n},() =>1);

	/*
	아래와 같이 하면 [ 0,1,2,3,4] 가 생성된다. v는 undefined임 
    var arr = Array.from({length:5},(v,i) =>i);
	*/
	
    reserve.forEach(function(item) { arr[item-1]++ });
    lost.forEach(function(item) { arr[item-1]-- });
    arr.forEach(function(item,idx) { 
        if(item == 0) {
            if(arr[idx-1]>1) answer++;
            else if(arr[idx+1]>1) { answer++; arr[idx+1]--; }
        }
        else answer++;
    });

    return answer;
}
```

```
// 다름사람 풀이
// 이해 안됨. solution(7, [2, 3, 4], [1, 2, 3, 6]); 일경우 통과못함
function solution(n, lost, reserve) {      
    return n - lost.filter(a => {
        const b = reserve.find(r => Math.abs(r-a) <= 1)
        if(!b) return true
        reserve = reserve.filter(r => r !== b)
    }).length
}
```







   
***
   

* K번째수
+ https://programmers.co.kr/learn/courses/30/lessons/42748?language=javascript


```
// 내소스
function solution(array, commands) {
    var answer = [];
    commands.forEach(function(arr) {
       answer.push(array.slice(arr[0]-1,arr[1]).sort(function(a,b) { return a-b; })[arr[2]-1]);
    });
    return answer;
}
```


```
// 내소스2
// forEach를 이렇게도 사용가능함. 
function solution(array, commands) {
    var answer = [];
    commands.forEach(arr => {
       answer.push(array.slice(arr[0]-1,arr[1]).sort((a,b) => a-b)[arr[2]-1]);
    });
    return answer;
}

```



   
***
***
   

* 2016년
+ https://programmers.co.kr/learn/courses/30/lessons/12901?language=javascript


```
// 내소스
function solution(a, b) {
    var answer = '';
    var week = ['SUN','MON','TUE','WED','THU','FRI','SAT'];
    var month =  [31,29,31,30,31,30,31,31,30,31,30,31];
    var tot = 5;
    for(let i=0;i<a-1;i++) tot += month[i]; 
    tot += b-1;
    answer = week[tot%7];
    return answer;
}
```


```
// 좀더 간략화된소스
function solution(a, b) {
    var week = ['SUN','MON','TUE','WED','THU','FRI','SAT'];
    var month =  [0,31,29,31,30,31,30,31,31,30,31,30,31];
    var tot = b+4;
    for(let i=1;i<a;i++) tot += month[i]; 
    return week[tot%7];
}
```

```
// 내장객체인 Date를 사용한다. 
// getDay()는 요일(0~6)을 리턴하는 함수
function solution(a, b) {
    var week = ['SUN','MON','TUE','WED','THU','FRI','SAT'];
    return week[(new Date('2016-'+a+'-'+b)).getDay()];
}
```

```
// 날짜를 String으로 변환하면, 앞의 3글자가 요일임. 
// 해당 요일을 대문자로 변환하여 리턴한다.
function solution(a, b) {
    return (new Date(2016,a-1,b)).toString().slice(0,3).toUpperCase();
}
```




   
***
   

* 3진법 뒤집기
+ https://programmers.co.kr/learn/courses/30/lessons/68935?language=javascript

```
function solution(n) {
    return parseInt(n.toString(3).split('').reverse().join(''),3);
}
```

```
function solution(n) {
    return parseInt([...n.toString(3)].reverse().join(''),3);
}
```

+ n.toString(3); // 3진수로 변환, n=45라면 1200
+ [...n.toString(3)] // 문자열을 모두 분리하여 배열로 변환 ["1", "2", "0", "0"]
+ [...n.toString(3)].reverse() // 배열을 반전시킨다. ["0", "0", "2", "1"]
+ [...n.toString(3)].reverse().join('') // 배열을 1개의 문자열로 합친다. "0021"
+ parseInt([...n.toString(3)].reverse().join(''),3) // 문자열을 3진수숫자로 취급하여, 10진수숫자로 변환한다.





   
***
   

* 같은 숫자는 싫어
+ https://programmers.co.kr/learn/courses/30/lessons/12906?language=javascript

```
function solution(arr)
{
    var answer = [];   
    arr.forEach((d,i) => { if(arr[i+1] != d) answer.push(d) });   
    return answer;
}
```


```
// 다른 사람의 풀이
// filter를 사용하여 두 값이 다를때 true를 리턴하게 한다. 
function solution(arr)
{
    return arr.filter((val,index) => val != arr[index+1]);
}
```



   
***
   

* 나누어 떨어지는 숫자 배열
+ https://programmers.co.kr/learn/courses/30/lessons/12910?language=javascript

```
function solution(arr, divisor) {
    var answer = [];
    answer = arr.filter( (d) => { return (d%divisor == 0); }).sort( (a,b) => { return a-b;}  );
    if(answer.length==0) answer.push(-1);
    return answer;
}
```


   
***
***
   

* 두 정수 사이의 합
+ https://programmers.co.kr/learn/courses/30/lessons/12912?language=javascript

```
// 내소스
function solution(a, b) {
    var answer = 0;    
    for(var i=(a<b?a:b);i<=(b>a?b:a);i++) answer += i;
    return answer;
}
```


```
// 다른사람 소스
function solution(a, b) {
    return (a+b)*(Math.abs(b-a)+1)/2;
}
```
