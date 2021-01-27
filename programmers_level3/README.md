# 프로그래머스 코딩 테스트 Level 3

* 네트워크
+ https://programmers.co.kr/learn/courses/30/lessons/43162?language=javascript


```javascript
// 내소스
function solution(n, computers) {
    var answer = 0;
    var arr = Array(n).fill(0);
    var index = 1;
    
    function fill(dst,src) {
        arr = arr.map( function(item) {
            if(item == dst) return src;
            return item;
        })
    }
    
    function connect(x,y) {
        if(arr[x] == 0 && arr[y] == 0) {
            arr[x] = arr[y] = index;
            index++;
        } else if(arr[x]==0) {
            arr[x] = arr[y];            
        } else if(arr[y] == 0) {
            arr[y] = arr[x];            
        } else {
            fill(arr[y],arr[x]);
        }   
    }
    
    computers.forEach( (d,i) => {
       d.forEach( (d2,j) => {
           if(i != j) {
               if(d2 == 1) {
                   connect(Math.min(i,j), Math.max(i,j));
               }
           }
       }) ;
    });
    
    let set = new Set();
    arr.forEach( (d) => { 
        if(d == 0) answer++;
        else set.add(d);
    });
    answer += set.size;
    
    return answer;
}
```

```javascript
// 다른사람소스
function solution(n, computers) {
    let arr;
    let visitArr;

    function dfs(i) {
        console.log(i);
        if(visitArr[i] == true) return 0;
        else visitArr[i] = true;

        for(let j in arr[i]) {
            if(arr[i][j] == 1)
                dfs(j);
        }

        return 1;
    }  
    
    let ctr = 0;
    arr = computers;
    visitArr = new Array(n).fill(false);

    for(let i in arr) {
        ctr += dfs(i);
    }
    console.log(visitArr);

    return ctr;
}
```

```javascript
// 개선된 소스
function solution(n, computers) {
    var answer = 0;
    var arr = Array(n).fill(false);
    
    function dfs(x) {
        if(arr[x] == true) return 0;
        arr[x] = true;        
        computers[x].forEach( (d,i) => {
           if(d==1) dfs(i); 
        });
        return 1;
    }
    
    arr.forEach( (d,i) => {
       answer += dfs(i); 
    });
    
    return answer;
}
```


* 단속카메라
+ https://programmers.co.kr/learn/courses/30/lessons/42884


```javascript
// 남의 소스
function solution(routes) {
  let answer = 0;
  // 차량의 진출지점을 기준으로 정렬을 수행한다. 
  routes.sort((a, b) => {
    return a[1] - b[1];
  });
  
  let camera = -30001;
  for (let i = 0; i < routes.length; i++) {
    if (camera < routes[i][0]) {
      answer++;
      camera = routes[i][1];
    }
  }
  return answer;
}
``` 



* 여행경로 (깊이/너비 우선 탐색)
+ https://programmers.co.kr/learn/courses/30/lessons/43164?language=javascript


```javascript
// 남의 소스
function solution(tickets) {
    var answer = [];
    var arr = Array(tickets.length).fill(0);
	var arrive = false;
	
	tickets.sort();    
	
    // ans : 방문한곳의 배열
	function rec(start, ans) {
		if(arrive === true) { 
			return;
		}

		ans.push(start);
		if(arr.indexOf(0) == -1) {
			answer = ans;
			arrive = true;
			return;
		}

		for(let i=0;i<arr.length;i++) {
			if(arr[i]===0 && tickets[i][0] === start) {
                // 재귀호출을 사용해서, 방문하지 않은곳이고, start에서 출발하는 ticket일경우, 1로 설정하고, 방문한다.
				arr[i] = 1;
                // ans.slice()를 해서 ans를 복제해야한다.
				rec(tickets[i][1],ans.slice());
				arr[i] = 0;
			}
		}
	}
	
	rec("ICN",[]);
	
    return answer;
}
``` 




* 단어 변환 (깊이/너비 우선 탐색)
+ https://programmers.co.kr/learn/courses/30/lessons/43163?language=javascript


```javascript
// 남의 소스
function solution(begin, target, words) {
    var answer = 999;
    var arr = Array(words.length).fill(false);

    function compare(a,b) {
        let cnt=0;
        for(let i=0;i<a.length&&cnt<2;i++)
            if(a.charAt(i)!=b.charAt(i)) cnt++;
        return cnt;
    }
    
    function rec(word,cnt) {
        if(cnt >= answer) return;
        if(word === target) {
            if(cnt<answer) answer = cnt;
            return;        
        }
        words.forEach( (d,i) => {
           if(arr[i] == false && compare(word,d) < 2) {
               arr[i] = true;
               rec(d,cnt+1);
               arr[i] = false;
           }
        });
    }
    
    rec(begin,0);
    if(answer == 999) answer = 0;
    
    return answer;
}
``` 





* 섬 연결하기 탐욕법(Greedy)
+ https://programmers.co.kr/learn/courses/30/lessons/42861?language=javascript

```javascript
// 남의 소스
function solution(n, costs) {
   var answer = 0;
   // 다리건설하는 비용을 오름차순으로 정렬한다. 
    var arr = Array.from({length:n}, (data,idx)=>idx);
    costs.sort( (a,b) => a[2]-b[2]);
    
    function fill(a,b) {
    	for(let i=0;i<arr.length;i++) {
    		if(arr[i] == b) arr[i] = a;
    	}

    }
    
    costs.forEach( (d) => {
        // 두 섬이 분리되어 있으면 연결한다. 
    	if(arr[d[0]] != arr[d[1]]) {
            // answer에 연결비용추가 
    		answer += d[2];
            //
    		fill(arr[d[0]],arr[d[1]]);
    	}
    });

    return answer;
}
``` 