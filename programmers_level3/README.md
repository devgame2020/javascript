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

