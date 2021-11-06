* 숫자 문자열과 영단어 : <https://programmers.co.kr/learn/courses/30/lessons/81301?language=java>
   
+ 내소스
```java
import java.util.Arrays;
import java.util.List;
class Solution {
    public int solution(String s) {
        String str="";
        List<String> arr_str = Arrays.asList("zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine");
        // String[] arr_str = {"zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"};
        
        String tmp="";
        for(int i=0;i<s.length();i++) {
            char c = s.charAt(i);           
            if(Character.isDigit(c) == true) 
                str += c;
            else {
                tmp += c;  // one
                // int idx = Arrays.asList(arr_str).indexOf(tmp);
                int idx = arr_str.indexOf(tmp);
                if(idx>=0) {
                    str += idx;
                    tmp="";                
                }                
            }
            
        }
        return Integer.parseInt(str);
    }
}
```


* 크레인 인형뽑기 게임 : <https://programmers.co.kr/learn/courses/30/lessons/64061>
   

+ 내소스
```java
import java.util.Stack;

class Solution {
    public int solution(int[][] board, int[] moves) {
        int answer = 0;
        Stack<Integer> stack = new Stack<>();
        
        for(int item:moves) {
            item--;
            for(int i=0;i<board.length;i++) {
                if(board[i][item] != 0) {
                    if(!stack.empty() && stack.peek() == board[i][item]) {
                        stack.pop();
                        answer += 2;
                    }
                    else 
                        stack.push(board[i][item]);
                    board[i][item] = 0;
                    break;                    
                }
            }
            
        }
        
        return answer;
    }
}
```


* [카카오 인턴] 키패드 누르기
+ https://programmers.co.kr/learn/courses/30/lessons/12937?language=javascript


+ 내소스
```java
class Solution {
    public String solution(int[] numbers, String hand) {
		int[] left = {3,0};
		int[] right = {3,2};
		
        String answer = "";
		final String Left = "L";
		final String Right = "R";   
        final int PY = 0;
        final int PX = 1;
        if(hand.compareTo("left") == 0) hand = Left;
        else hand = Right;
		
        int[] loc = {0,0};
        String ans = Left;
        
        for(int d:numbers) {
            loc[PY] = d==0?3:(d-1)/3;
            loc[PX] = d==0?1:(d-1)%3;
            
            if(loc[PX] == 0) 
            	ans = Left;
            else if(loc[PX] == 2)
            	ans = Right;
            else {           
            	int left_len = Math.abs(loc[PX]-left[PX]) + Math.abs(loc[PY]-left[PY]); 
            	int right_len = Math.abs(loc[PX]-right[PX]) + Math.abs(loc[PY]-right[PY]);
                
            	if(left_len<right_len) 
            		ans = Left;
            	else if(left_len>right_len) 
            		ans = Right;
            	else
            		ans = hand;
            }
            
            answer += ans;
            if(ans == Left) 
                left = loc.clone();
            else 
                right = loc.clone();
        }
        
        return answer;
    }
}
```





* 없는 숫자 더하기
+ https://programmers.co.kr/learn/courses/30/lessons/86051?language=java


+ 내소스
```java
class Solution {
    public int solution(int[] numbers) {
        int answer = 0;
        for(int d:numbers) answer += d;
        return 45-answer;
    }
}
```



* 음양 더하기
+ https://programmers.co.kr/learn/courses/30/lessons/86051?language=java


+ 내소스
```java
class Solution {
    public int solution(int[] absolutes, boolean[] signs) {
        int answer = 0;
        for(int i=0;i<absolutes.length;i++)
            answer += signs[i]?absolutes[i]:-absolutes[i];
        return answer;
    }
}
```



* 내적
+ https://programmers.co.kr/learn/courses/30/lessons/70128?language=java


+ 내소스
```java
class Solution {
    public int solution(int[] a, int[] b) {
        int answer = 0;
        for(int i=0;i<a.length;i++)
            answer += a[i] * b[i];
        return answer;
    }
}
```

