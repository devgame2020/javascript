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
    moves.forEach(function(item) {
        for(var i=0;i<len;i++) {
            if(board[i][item-1] != 0) {
                if(arr.length && arr[arr.length-1] == board[i][item-1]) {
                    arr.pop();
                    answer += 2;
                }
                else 
                    arr.push(board[i][item-1]);
                board[i][item-1] = 0;
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
```

+ 다른사람소스 

```
```
