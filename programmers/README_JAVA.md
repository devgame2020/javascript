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



* K번째수
+ https://programmers.co.kr/learn/courses/30/lessons/42748


+ 내소스
```java
public class KstNumber {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        int idx =0;
        for(int i=0;i<commands.length;i++) {
            int[] arr = commands[i];
            int[] tmp = Arrays.copyOfRange(array,arr[0]-1,arr[1]);
            Arrays.sort(tmp);            
            answer[idx++] = tmp[arr[2]-1];
        }
        return answer;
    }
}
```



* 완주하지 못한 선수
+ https://programmers.co.kr/learn/courses/30/lessons/42576


+ 내소스
```java
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

public class UnfinishedPlayer {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        Map<String,Integer> map1 = new HashMap<>();
        for(String d:participant) {
            if(map1.get(d) == null)
                map1.put(d,1);
            else
                map1.put(d,map1.get(d)+1);
        }
        for(String d:completion) {   
            map1.put(d,map1.get(d)+1);            
        }

        Iterator<String> mapIter = map1.keySet().iterator();
        while(mapIter.hasNext()){
            String key = mapIter.next();
            int value = map1.get( key );
            if(value % 2 == 1) return key;
        }

        return answer;
    }
}
```



* 소수만들기
+ https://programmers.co.kr/learn/courses/30/lessons/12977


+ 내소스
```java
public class MakePrimeNumber {
    public boolean isPrime(int num) {
        for(int i=2;i<num;i++)
            if(num%i == 0) return false;
        return true;
    }

    public int solution(int[] nums) {
        int answer = 0;

        for(int i=0;i<nums.length;i++) 
            for(int j=i+1;j<nums.length;j++)
                for(int k=j+1;k<nums.length;k++) 
                    if(isPrime(nums[i]+nums[j]+nums[k])) answer++;

        return answer;
    }
}
```




* 모의고사
+ https://programmers.co.kr/learn/courses/30/lessons/42840?language=java#


+ 내소스
```java
import java.util.ArrayList;

class Solution { 
    public int[] solution(int[] answers) {
        int[][] arr = {{},{1,2,3,4,5},{2,1,2,3,2,4,2,5},{3,3,1,1,2,2,4,4,5,5}};
        int[] jumsu = { 0,0,0,0 };
        
        for(int idx=0;idx<answers.length;idx++) {
        	for(int i=1;i<=3;i++) {
        		if(answers[idx] == arr[i][idx%arr[i].length])
                    
					jumsu[i]++;
        	}
        }  
      
        int max = Math.max(jumsu[1], Math.max(jumsu[2],jumsu[3]));
        
        int cnt = 0;
        for(int i=1;i<=3;i++)  {
            if(max == jumsu[i]) cnt++;
        }        
        
        int idx = 0;
        int[] answer = new int[cnt];
        for(int i=1;i<=3;i++) 
        	if(max == jumsu[i])
        		answer[idx++] = i;

       return answer;   
    }
}
```




* 체육복
+ https://programmers.co.kr/learn/courses/30/lessons/42862?language=java


+ 내소스
```java
import java.util.Arrays;
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int answer = 0;
        int[] arr = new int[n];
        Arrays.fill(arr, 1);
        
        for(int d:reserve) arr[d-1]++;
        for(int d:lost) arr[d-1]--;
        for(int i=0;i<arr.length;i++) {
        	if(arr[i] == 0) {
        		if(i>0 && arr[i-1]>1) answer++;
        		else if(i<arr.length-1 && arr[i+1]>1) { 
        			answer++;
        			arr[i+1]--;
        		}
        	}
        	else 
        		answer++;
        }
        
        return answer;
    }
}
```






* 폰켓몬
+ https://programmers.co.kr/learn/courses/30/lessons/1845?language=java


+ 내소스
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int solution(int[] nums) {
        int answer = 0;      
        int cnt = nums.length/2;
        Set<Integer> set = new HashSet<>();
        for(int d:nums) set.add(d);
        if(cnt<set.size()) answer = cnt;
        else answer = set.size();
        return answer;
    }
}
```





* 실패율
+ https://programmers.co.kr/learn/courses/30/lessons/42889?language=java


+ 내소스
```java

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

class Node {
    public int no;
    public float fail;
    
    Node(int i,float f) {
        no = i;
        fail = f;
    }
}

class NodeCompare implements Comparator<Node> {
	
	public int compare(Node a, Node b) {
		if(a.fail < b.fail)
			return 1;
		else if(a.fail > b.fail)
			return -1;
		return 0;
	}
}

class Solution {
    public int[] solution(int N, int[] stages) {
        List<Node> fail = new ArrayList<Node>();
        int cnt = stages.length;
        int[] answer = new int[N];
        int[] arr = new int[N+2];
        Arrays.fill(arr, 0);   
        for(int d:stages) arr[d]++;
        for(int i=1;i<=N;i++) {
            fail.add(new Node(i,(float)arr[i]/cnt));
            cnt -= arr[i];
        }
        
        Collections.sort(fail, new NodeCompare());        
        int i=0;
        for(Node d:fail) {
        	answer[i++] = d.no;
        }
        
        return answer;
    }
}
```





* 약수의 개수와 덧셈
+ https://programmers.co.kr/learn/courses/30/lessons/77884?language=java


+ 내소스
```java
class Solution {
    public int solution(int left, int right) {
        int answer = 0;
        for(int i=left;i<=right;i++) {
            int cnt = 1;
            for(int j=1;j<=i/2;j++) {
                if(i%j == 0) cnt++;
            }
            answer += cnt%2==0?i:-i;
        }        
        return answer;
    }
}
```


* 3진법 뒤집기
+ https://programmers.co.kr/learn/courses/30/lessons/68935?language=java


+ 내소스
```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        StringBuffer str = new StringBuffer();
        while(n>0) {
        	str.append(""+n%3);
            n /= 3;
        }
        answer = Integer.parseInt(str.toString(),3);
        return answer;
    }
}
```
















