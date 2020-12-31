# 프로그래머스 코딩 테스트


* 가운데 글자 가져오기 : <https://programmers.co.kr/learn/courses/30/lessons/12903>
   
+ 내소스
```javascript
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
```javascript
function solution(s) {
    return s.substr(Math.ceil(s.length / 2) - 1, s.length % 2 === 0 ? 2 : 1);
}
```
   
***
   
* 크레인 인형뽑기 게임 : <https://programmers.co.kr/learn/courses/30/lessons/64061>
   

+ 내소스
```javascript
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
```javascript
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

```javascript
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

```javascript
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

```javascript
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


```javascript
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


```javascript
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

```javascript
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


```javascript
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

```javascript
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

```javascript
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

```javascript
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


```javascript
// 내소스
function solution(array, commands) {
    var answer = [];
    commands.forEach(function(arr) {
       answer.push(array.slice(arr[0]-1,arr[1]).sort(function(a,b) { return a-b; })[arr[2]-1]);
    });
    return answer;
}
```


```javascript
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


```javascript
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


```javascript
// 좀더 간략화된소스
function solution(a, b) {
    var week = ['SUN','MON','TUE','WED','THU','FRI','SAT'];
    var month =  [0,31,29,31,30,31,30,31,31,30,31,30,31];
    var tot = b+4;
    for(let i=1;i<a;i++) tot += month[i]; 
    return week[tot%7];
}
```

```javascript
// 내장객체인 Date를 사용한다. 
// getDay()는 요일(0~6)을 리턴하는 함수
function solution(a, b) {
    var week = ['SUN','MON','TUE','WED','THU','FRI','SAT'];
    return week[(new Date('2016-'+a+'-'+b)).getDay()];
}
```

```javascript
// 날짜를 String으로 변환하면, 앞의 3글자가 요일임. 
// 해당 요일을 대문자로 변환하여 리턴한다.
function solution(a, b) {
    return (new Date(2016,a-1,b)).toString().slice(0,3).toUpperCase();
}
```




   
***
   

* 3진법 뒤집기
+ https://programmers.co.kr/learn/courses/30/lessons/68935?language=javascript

```javascript
function solution(n) {
    return parseInt(n.toString(3).split('').reverse().join(''),3);
}
```

```javascript
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

```javascript
function solution(arr)
{
    var answer = [];   
    arr.forEach((d,i) => { if(arr[i+1] != d) answer.push(d) });   
    return answer;
}
```


```javascript
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

```javascript
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

```javascript
// 내소스
function solution(a, b) {
    var answer = 0;    
    for(var i=(a<b?a:b);i<=(b>a?b:a);i++) answer += i;
    return answer;
}
```


```javascript
// 다른사람 소스
function solution(a, b) {
    return (a+b)*(Math.abs(b-a)+1)/2;
}
```



* 문자열 내 마음대로 정렬하기
+ https://programmers.co.kr/learn/courses/30/lessons/12915?language=javascript#

```javascript
// 내소스
function solution(strings, n) {
    var answer = [];
    answer = strings.sort( (a,b) => {  
        if(a[n] == b[n]) return a>b?1:-1;
        return a[n] > b[n]?1:-1 
    });
    return answer;
}
```


```javascript
// 다른사람소스
// localCompare()를 사용하여 더 간결하게 표현함
function solution(strings, n) {
    // strings 배열
    // n 번째 문자열 비교
    return strings.sort((s1, s2) => s1[n] === s2[n] ? s1.localeCompare(s2) : s1[n].localeCompare(s2[n]));
}
```


* 문자열 내 p와 y의 개수
+ https://programmers.co.kr/learn/courses/30/lessons/12916

```javascript
// 내소스
// 모두 대문자로 변환하고, 정규식을 사용하여 처리했다.
function solution(s){
    var answer = true;
    s = s.toUpperCase();
    var p = s.match(/P/g);   
    var y = s.match(/Y/g);
    if((p?p.length:0) != (y?y.length:0))  
        answer = false;
    return answer;
}
```


```javascript
// 개선된소스
function solution(s){
    var p = s.match(/P/ig);   
    var y = s.match(/Y/ig);
    return ((p?p.length:0) == (y?y.length:0));
}
```


```javascript
// 다른 사람 소스
// 왜 이게 정답인지 이해안감.
return s.toUpperCase().split("P").length === s.toUpperCase().split("Y").length;

// 정규식 ig => g:글로벌,전역매칭  i:대소문자 구분안함
// 문제가 있음. 해당 문자가 없을경우 NULL을 리턴하는데 length사용시 런타임 오류발생
return s.match(/p/ig).length == s.match(/y/ig).length;
```


* https://programmers.co.kr/learn/courses/30/lessons/12917
+ 문자열 내림차순으로 배치하기

```javascript
// 내소스
function solution(s) {
    var answer = '';   
    answer = [...s].sort().reverse().join('');
    return answer;
}
```

```javascript
// sort할때 역순으로 정렬함
function solution(s) {
    var answer = '';
    
    var a = [...s].sort(function(a,b) { 
        if(a>b) return -1;
        if(b>a) return 1;
        return 0;
        
        /* debug용 코드
        console.log(a+":"+b );
        if (a > b) { console.log(a + " 가 더 크다"); return -1; }
        if (b > a) { console.log(b + " 가 더 크다"); return 1; }
        console.log("0");
        return 0;        
        */
    } );
    answer = a.join('');
    
//    answer = [...s].sort().reverse().join('');
    return answer;
}
```


```javascript
// 다른 사람의 소스
function solution(s) {
    return s.split('').sort((a, b) => {
        if (a > b) return -1;
        if (b > a) return 1;
        return 0;
    }).join('');
}
```




   
***
***
   



* 문자열 다루기 기본
+ https://programmers.co.kr/learn/courses/30/lessons/12918?language=javascript



```javascript
// 내소스 : 일부는 실패가 나옴 
// 0.01 , 1e22같은 경우일때 이건 숫자만 구성된것인가, 아니면 문자인것인가?
// 문제의 정의가 명확하지 않음
function solution(s) {
    return (!isNaN(s) && (s.length==4 || s.length==6));
}
```



```javascript
// forEach를 사용하여 0~9인값이 있을경우에만 숫자로 인정함. 
function solution(s) {
    var is = true;
    [...s].forEach( function(d) { if(d<"0" || d>"9") is=false; });
    return (is && (s.length==4 || s.length==6));
}
```






* 문자열 내림차순으로 배치하기
+ https://programmers.co.kr/learn/courses/30/lessons/12917?language=javascript

```javascript
// 내풀이
// 문자열 s를 [...s] 를 사용하여 배열로 만들고, sort()로 정렬, reverse()로 역순으로 뒤집고, join()으로 다시 문자열을 만들어 리턴한다.
function solution(s) {
    return [...s].sort().reverse().join('');
}
```

```javascript
// 정렬할때 아예 역순으로 정렬한다.
function solution(s) {
    var answer = '';
    
    var a = [...s].sort(function(a,b) { 
        if(a>b) return -1;
        if(b>a) return 1;
        return 0;
        
        /*
        console.log(a+":"+b );
        if (a > b) { console.log(a + " 가 더 크다"); return -1; }
        if (b > a) { console.log(b + " 가 더 크다"); return 1; }
        console.log("0");
        return 0;        
        */
    } );
    answer = a.join('');
    
//    answer = [...s].sort().reverse().join('');
    return answer;
}
```


* 소수 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/12921?language=javascript

```javascript
// 내소스
// 에라토스테네스의체를 이용하였다.
function solution(n) {
    var answer = 0;
    var arr = [];
    for(var i=2;i<=n;i++) {
        if(arr[i] == null) {                   
            arr[i] = 1;
            for(var j=i*2;j<=n;j+=i) arr[j] = 0; 
        }
    }
    arr.forEach(function(d,i) { if(d) answer++; });
    return answer;
}
```

* 수박수박수박수박수박수?
+ https://programmers.co.kr/learn/courses/30/lessons/12922?language=javascript

```javascript
// 내소스
function solution(n) {
    var answer = '';
    for(var i=0;i<n;i++) answer += (i%2?"박":"수");
    return answer;
}
```



   
***
***
   



* 문자열을 정수로 바꾸기
+ https://programmers.co.kr/learn/courses/30/lessons/12925?language=javascript

```javascript
// 내소스
function solution(s) {
    var answer = 0;
    answer = parseInt(s);
    return answer;
}
```



