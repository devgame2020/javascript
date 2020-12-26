# 프로그래머스 코딩 테스트


+ 가운데 글자 가져오기
+ https://programmers.co.kr/learn/courses/30/lessons/12903

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

