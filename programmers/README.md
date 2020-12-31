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



* 내적
+ https://programmers.co.kr/learn/courses/30/lessons/70128?language=javascript

```javascript
function solution(a, b) {
    var answer = 0;
    a.forEach( (d,i) => answer += (d * b[i]));
    return answer;
}
```

* 시저 암호
+ https://programmers.co.kr/learn/courses/30/lessons/12926?language=javascript

```javascript
// 내소스
function solution(s, n) {
    var answer = '';
    // 65~90 : A~Z
    // 97~122 : a~z
    // 32 : space

	var base = 65;    
    var arr = [];
    for(var i=0;i<s.length;i++) {
        var x = s.charCodeAt(i);
        // Space는 변환안함
    	if(x == 32) {
    		arr.push(' '); 
    		continue;
    	}
    	base = x<=90?65:97;
   		arr.push(String.fromCharCode(base + ((s.charCodeAt(i)+n-base) % 26)));	
    }
    answer = arr.join('');
    return answer;
}
```

* 약수의 합
+ https://programmers.co.kr/learn/courses/30/lessons/12928?language=javascript

```javascript
// 내소스
function solution(n) {
    var answer = n<2?n:1+n;
    for(var i=2;i<=parseInt(n/2);i++) {
        answer+=(n%i==0?i:0);
    }
    return answer;
}
```


   
***
***
   



* 이상한 문자 만들기
+ https://programmers.co.kr/learn/courses/30/lessons/12930?language=javascript

```javascript
// 내소스
function solution(s) {
    var answer = '';
    var ret = s.split(" ");
    ret.forEach( function(d,i) { 
    	var str = "";
    	[...d].forEach( function(d2,i2) {
    		if(i2%2==0) 
	    		str += d2.toUpperCase();
    		else 
    			str += d2.toLowerCase();
    	});
    	ret[i] = str;
    });
    answer = ret.join(' ');
    return answer;
}
```

```javascript
// 내소스 : 속도가 이게 더 빠를것같음.
function solution(s) {
    var answer = '';
    var idx = 0;
    for(var i=0;i<s.length;i++) {
    	s[i] == ' '?idx = 0:idx++;
    	if(idx%2 == 1) 
    		answer += s[i].toUpperCase();
    	else
    		answer += s[i].toLowerCase();
    }
    return answer;
}
```


* 자릿수 더하기
+ https://programmers.co.kr/learn/courses/30/lessons/12931?language=javascript

```javascript
// 내소스
function solution(n)
{
    var answer = 0;  
    // n을 문자열로 변경해서,
    // 배열로 만든후
    // forEach로 각각의 값들을 모두 정수로 변환하여 더한다.
    [...(""+n)].forEach((d)=> answer += parseInt(d)); 
    return answer;
}
```


* 자연수 뒤집어 배열로 만들기
+ https://programmers.co.kr/learn/courses/30/lessons/12932?language=javascript

```javascript
// 내소스
function solution(n) {
    var answer = [];
    // n을 문자열로 변경후
    // 배열로 만들어서, 반전을 시킨후
    // forEach로 한개씩 숫자로 변환하여 answer에 push한다.
    [...(""+n)].reverse().forEach( (d) => answer.push(parseInt(d)));
    return answer;
}
```


* 정수 내림차순으로 배치하기
+ https://programmers.co.kr/learn/courses/30/lessons/12933?language=javascript

```javascript
// 내소스
function solution(n) {
    var answer = 0;
    answer = parseInt([...n.toString()].sort().reverse().join(''));
    return answer;
}
```



   
***
***
   

* 정수 제곱근 판별
+ https://programmers.co.kr/learn/courses/30/lessons/12934?language=javascript

```javascript
// 내소스
function solution(n) {
    var answer = -1;
    var sqrt = parseInt(Math.sqrt(n));
    if(sqrt*sqrt == n) answer = (sqrt+1)*(sqrt+1);
    return answer;
}
```

***
***
   

* 제일 작은 수 제거하기
+ https://programmers.co.kr/learn/courses/30/lessons/12935?language=javascript

```javascript
// 내소스
function solution(arr) {
    var answer = [];
    if(arr.length==1) return [-1];
    var max = 0;
    arr.forEach( function(d,i) {        
        if(d < arr[max]) max = i;    
    });
    arr.forEach( function(d,i) {
        if(i!=max) answer.push(d);
    });
    
    return answer;
}
```


```javascript
// 다른 사람 소스 
function solution(arr) {
    // Math.min(...arr) ==> arr 배열의 가장 작은 값을 리턴한다.
    // splice(인덱스, 1) : 해당 배열의 인덱스위치에서 1개의 요소를 삭제한다. 
    // indexOf(배열값) : 해당 배열의 배열값이 있는 index를 얻는다.
    arr.splice(arr.indexOf(Math.min(...arr)),1);
    if(arr.length<1)return[-1];
    return arr;
}
```

```javascript
// 내소스2
function solution(arr) {
    // arr배열의 최소값을 구한다.
    var min = Math.min(...arr);  
    // min값이 있는 배열의 인덱스를 구한다.  
    var idx = arr.indexOf(min)
    // arr배열의 idx번째위치에서 1개의 요소를 삭제한다.
    arr.splice(idx,1);
    if(arr.length<1) return [-1];
    return arr;
}
```

* 짝수와 홀수
+ https://programmers.co.kr/learn/courses/30/lessons/12937?language=javascript

```javascript
function solution(num) {
    var answer = num%2==0?"Even":"Odd";
    return answer;
}
```



* [카카오 인턴] 키패드 누르기
+ https://programmers.co.kr/learn/courses/30/lessons/12937?language=javascript


```javascript
// 내소스
// 좌표 : [ 행,열 ]
function solution(numbers, hand) {
    const Left = "L";
    const Right = "R";
    var answer = '';
    var arr = [ [1,2,3], [4,5,6], [7,8,9], ['*',0,'#' ] ];
    var l = [ 3, 0 ]; 
    var r = [ 3, 2 ];
    var ans = Left;    
  
    numbers.forEach( function(d) { 
        // 해당번호의 좌표를 찾는다.(loc)
        var loc = [0,0];
        for(var i=0;i<arr.length;i++) {
            var idx = arr[i].indexOf(d);
            if(idx >=0) loc = [i,idx];
        }
        
        // 어느쪽손이 더 가까운지 확인한다.
        if(loc[1] == 0) 
            ans = Left;
        else if(loc[1] == 2) 
            ans = Right;           
        else {
            let left_len = Math.abs(loc[0]-l[0]) + Math.abs(loc[1]-l[1]);
            let right_len = Math.abs(loc[0]-r[0]) + Math.abs(loc[1]-r[1]);
            if(left_len<right_len) 
                ans = Left;
            else if(left_len>right_len) 
                ans = Right;
            else 
                ans = hand=="right"?Right:Left;
        }
         
        // 더 가까운손이 이동한다.
        if(ans == Left) { 
            answer += Left;
            l = loc;
        }
        else {
            answer += Right;
            r = loc;            
        }
    });
    
    return answer;
}
```


   
***
***
   


* 최대공약수와 최소공배수
+ https://programmers.co.kr/learn/courses/30/lessons/12940?language=javascript


```javascript
// 내소스
// 최대공약수를 구한다.
function gcdFunc(a,b) {
    // 유클리드 호제법
    while(b>0)     {
        var tmp = b;
        b = a%b;
        a = tmp;
    }
    return a;
}

function solution(n, m) {
    var gcd = gcdFunc(n,m);
    // 최소공배수는 두수를 곱한값에 최대공약수로 나눈다.
    var lcd = n*m/gcd;
    return [gcd,lcd];
}
```


* 콜라츠 추측
+ https://programmers.co.kr/learn/courses/30/lessons/12943?language=javascript


```javascript
// 내소스
function solution(num) {
    var answer = -1;
    for(var i=0;i<500;i++) {        
        if(num==1) return i;
        if(num%2==0) num/=2;
        else num= num*3+1;
    }
    return answer;
}
```


```javascript
// 다른사람 소스
function collatz(num,count = 0) {
    return num == 1 ? (count >= 500 ? -1 : count) : collatz(num % 2 == 0 ? num / 2 : num * 3 + 1,++count);
}

function solution(num) {
    return collatz(num);
}
```


* 평균 구하기
+ https://programmers.co.kr/learn/courses/30/lessons/12944?language=javascript


```javascript
// 내소스
function solution(arr) {
    var answer = 0;
    arr.forEach( (d) => answer+=d );
    return answer/arr.length;
}
```


```javascript
// 다른사람소스
function solution(arr) {
    return array.reduce((a, b) => a + b) / array.length;
}
```

* 하샤드 수
+ https://programmers.co.kr/learn/courses/30/lessons/12947?language=javascript


```javascript
// 내소스
function solution(x) {
    return x % [...x.toString()].reduce( (p,d,i) => parseInt(p)+parseInt(d) ) == 0
}
```


   
***
***
   



* 핸드폰 번호 가리기
+ https://programmers.co.kr/learn/courses/30/lessons/12948?language=javascript


```javascript
// 내소스
function solution(phone_number) {
    var answer = '';
    answer = "*".repeat(phone_number.length-4) +  phone_number.substring(phone_number.length-4);
    return answer;
}
```

```javascript
// 다른사람 소스
// 정규식으로 풀었다.
function solution(phone_number) {
    return phone_number.replace(/\d(?=\d{4})/g, "*");
}
```






* 행렬의 덧셈
+ https://programmers.co.kr/learn/courses/30/lessons/12950?language=javascript


```javascript
// 내소스
function solution(arr1, arr2) {
    var answer = [];
    arr1.forEach( function(d,i) {
        var tmp = arr2[i];
        var ans = [];
        for(var i=0;i<tmp.length;i++)
            ans.push(d[i] + tmp[i]);
        answer.push(ans);
    });
    
    return answer;
}
```

```javascript
// 다른사람 소스
function solution(arr1, arr2) {
    return arr1.map((a,i) => a.map((b, j) => b + arr2[i][j]));
}    
```



* x만큼 간격이 있는 n개의 숫자
+ https://programmers.co.kr/learn/courses/30/lessons/12954?language=javascript


```javascript
// 내소스
function solution(x, n) {
    var answer = [];
    for(var i=1;i<=n;i++) answer.push(x*i);
    return answer;
}
```

```javascript
// 다른사람소스
// x로 배열을 채우고, map을 사용해서 값을 조정하였다.
function solution(x, n) {
    return Array(n).fill(x).map((v, i) => (i + 1) * v)
}
```


* 직사각형 별찍기
+ https://programmers.co.kr/learn/courses/30/lessons/12969?language=javascript


```javascript
// 내소스
process.stdin.setEncoding('utf8');
process.stdin.on('data', data => {
    const n = data.split(" ");
    const a = Number(n[0]), b = Number(n[1]);
    
    var star = "*".repeat(a);
    for(var i=0;i<b;i++)
        console.log(star);
        
});
```




   
***
***
   



* 예산
+ https://programmers.co.kr/learn/courses/30/lessons/12982?language=javascript


```javascript
// 내소스
// 오류가 나옴..원인불명.
function solution(d, budget) {
    var answer = 0;
    /////////////////////////////
    // 이렇게 하면 일부문제 오류발생
    var arr = d.sort();
    // 이렇게 하면 정상작동.
    var arr = d.sort(function(a, b) {
        return a - b;
    });    
    //////////////////////////////
    var sum = 0;
    for(var i=0;i<arr.length;i++) {
        sum += arr[i];
        if(budget>=sum) answer++;
    }    
    return answer;
}
```

```javascript
// 다른사람 소스
function solution(d, budget) {
    var count = 0;
    var sum = 0;
    
    d.sort(function(a, b) {
        return a - b;
    });
    
    for(var i=0; i < d.length; i++) {
        count++;
        sum += d[i];
        if(sum > budget) {
            count--;
            break;
        }
    }
    return count;    
}
```




* [1차] 비밀지도
+ https://programmers.co.kr/learn/courses/30/lessons/17681?language=javascript


```javascript
// 내소스
function solution(n, arr1, arr2) {  
    var answer = [];
    for(var i=0;i<n;i++) {
        var x = (arr1[i] | arr2[i]).toString(2);
        answer.push(" ".repeat(n-x.length) + x.replace(/0/g," ").replace(/1/g,"#"));
    }
    return answer;
}
```

```javascript
// 다른사람 소스
function solution(n, arr1, arr2) {  
    return arr1.map((i, index) =>('0'.repeat(n) + (i | arr2[index]).toString(2)).slice(-n)).map(i => i.replace(/0/g, ' ').replace(/1/g, '#'));
}
```


* 실패율
+ https://programmers.co.kr/learn/courses/30/lessons/42889?language=javascript


```javascript
// 내소스
function solution(N, stages) {
    var answer = [];
    var arr = [];
    for(var i=1;i<=N;i++) {
        var tot = 0;
        var fail=0;
        stages.forEach( function(d) { 
            if(d>=i) tot++;
            if(d==i) fail++;
        });
        
        arr.push( [ i,fail==0?0:fail/tot ]);
    }
    arr = arr.sort( function(a,b)  {
        if(a[1] == b[1]) return a[0]-b[0];
        return b[1] - a[1];
    });
    arr.forEach( (d) => answer.push(d[0]));
    return answer;
}
```







* [1차] 다트 게임
+ https://programmers.co.kr/learn/courses/30/lessons/17682?language=javascript


```javascript
// 내소스
function solution(dartResult) {
    var answer = 0;
    var idx = 0;
    var arr = [];
        
    var data="";
    for(var i=0;i<dartResult.length;) {        
        var d = [ ...dartResult.substring(i,i+4)];             
        var num = 0;
        var b = '';
        var opt = '';
        if(d[1] == '0') { 
            num = parseInt(d[0]+d[1]);
            b = d[2];
            if(d[3] == '#' || d[3] == '*') {
                opt = d[3];
                i+=4;                
            }
            else
                i+=3;
        }
        else { 
            num = parseInt(d[0])
            b = d[1];
            if(d[2] == '#' || d[2] == '*') {
                opt = d[2];
                i+=3;                
            }
            else
                i+=2;
                
        }            
        
        arr.push( [num,b,opt] );
    }
    
    var jumsu = [];
    arr.forEach( function(d,i) {
        var score = parseInt(d[0]);
        if(d[1] == 'D') score = Math.pow(score,2);
        else if(d[1] == 'T') score = Math.pow(score,3);        
        jumsu[i] = score;
        
        if(d[2] == '*') {
            jumsu[i] = score*2;
            if(i>0) jumsu[i-1] = jumsu[i-1]*2;
        }
        else if(d[2] == '#') {
            jumsu[i] = -score;
        }
    });
    jumsu.forEach( (d) => answer+=d );
    
    return answer;
}
```


```javascript
// 개선된 소스
function solution(dartResult) {    
    var answer = 0;
    var idx = 0;
    var arr = [];
        
    var data="";
    for(var i=0;i<dartResult.length;) {        
        var d = [ ...dartResult.substring(i,i+4)];             
        
        var nsize=1;
        if(d[1] == '0') nsize=2;
        
        var b = 1;
        if(d[nsize] == 'D') b = 2;
        else if(d[nsize] == 'T') b = 3;

        var opt = 1;
        if(d[nsize+1] == '*') opt = 2;
        else if(d[nsize+1] == '#') opt = -1;
        
        if(opt!=1) i+=nsize+2;
        else i+=nsize+1;    
        
        arr.push( [parseInt(d.join('').substring(0,nsize)),b,opt] );
    }
    
    var jumsu = [];
    arr.forEach( function(d,i) {
        jumsu[i] = Math.pow(parseInt(d[0]),d[1])*d[2];        
        if(d[2] == 2 && i>0) jumsu[i-1] = jumsu[i-1]*d[2];

    });
    jumsu.forEach( (d) => answer+=d );
    
    return answer;
}
```

```javascript
// 더 개선된 소스
function solution(dartResult) {    
    var answer = 0;
    var idx = 0;
    var arr = [];
    const bonus = [ 0, 'S', 'D', 'T'];
        
    var data="";
    for(var i=0;i<dartResult.length;) {        
        var d = [ ...dartResult.substring(i,i+4)];             
        
        var nsize=1;
        if(d[1] == '0') nsize=2;
        
        var opt = 1;
        if(d[nsize+1] == '*') opt = 2;
        else if(d[nsize+1] == '#') opt = -1;
        
        if(opt!=1) i+=nsize+2;
        else i+=nsize+1;    
        
        arr.push( [parseInt(d.join('').substring(0,nsize)),bonus.indexOf(d[nsize]),opt] );
    }
    
    var jumsu = [];
    arr.forEach( function(d,i) {
        jumsu[i] = Math.pow(parseInt(d[0]),d[1])*d[2];        
        if(d[2] == 2 && i>0) jumsu[i-1] = jumsu[i-1]*d[2];

    });
    jumsu.forEach( (d) => answer+=d );
    
    return answer;
}
```

   
***
***
   

