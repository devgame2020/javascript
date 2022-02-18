

* 문자열 다루기 기본
+ https://programmers.co.kr/learn/courses/30/lessons/12918

+ 내소스
```c#
class Solution {
    public boolean solution(String s) {
        if(s.length() != 4 && s.length() != 6) return false;
        for(int i=0;i<s.length();i++) {
            if(s.charAt(i) <'0' || s.charAt(i) >'9') return false;
        }
        return true;
    }
}
```



* 서울에서 김서방 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/12919

+ 내소스
```c#
using System;

public class Solution {
    public string solution(string[] seoul) {
        return String.Format("김서방은 {0}에 있다",Array.IndexOf(seoul, "Kim"));
    }
}
```




* 소수 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/12921

+ 내소스
```c#
public class Solution {
    public int solution(int n) {
        int answer = 0;
        int[] arr = new int[n+1];
        for(int i=2;i<=n;i++) {
            if(arr[i] == 2) continue;
            arr[i] = 1;
            for(int j=i*2;j<=n;j+=i) {
                arr[j] = 2;
            }
        }
        for(int i=2;i<=n;i++) 
            if(arr[i] == 1) answer++;        
        return answer;
    }
}
```
