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


* 프로그래머스 Level 1,최소직사각형
+ https://programmers.co.kr/learn/courses/30/lessons/86491



+ 내소스
```java
// 프로그래머스 Level 1,최소직사각형
public class minimumrectangle {
    public int solution(int[][] sizes) {
        int x=0,y=0;
        for(int []d:sizes) {
            if(d[0]>d[1]) {
                x = Math.max(x, d[0]);
                y = Math.max(y, d[1]);
            }
            else {
                x = Math.max(x, d[1]);
                y = Math.max(y, d[0]);
            }
        }
        return x*y;
    }
}
```


* 프로그래머스 Level 1,나머지가 1이 되는 수 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/87389?language=java



+ 내소스
```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        for(int i=2;i<=n;i++)
            if((n-1)%i == 0) return i;
        return answer;
    }
}
```




* 프로그래머스 Level 1,부족한 금액 계산하기
+ https://programmers.co.kr/learn/courses/30/lessons/82612


```javascript
// 내소스
class Solution {
    public long solution(int price, int money, int count) {
        long sum = (long)price*((count+1)*(count/2)+(count+1)/2*(count%2));
        return sum>money?sum-money:0;
    }
}
```





* 프로그래머스 Level 1,[1차] 비밀지도
+ https://programmers.co.kr/learn/courses/30/lessons/17681?language=java


```javascript
// 내소스
class Solution {
    public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] answer = new String[n];
        for(int i=0;i<n;i++) {
            int d = arr1[i] | arr2[i];
            String str = Integer.toBinaryString(d).replaceAll("1","#").replaceAll("0"," ");
            answer[i] = " ".repeat(n-str.length()) + str;
        }
        return answer;
    }
}
```



* 프로그래머스 Level 1,가운데 글자 가져오기
+ https://programmers.co.kr/learn/courses/30/lessons/12903


```javascript
// 내소스
class Solution {
    public String solution(String s) {
        return s.substring((s.length()-1)/2, (s.length()-1)/2 + 2 - s.length()%2);
    }
}
```



* 프로그래머스 Level 1,[1차] 다트 게임
+ https://programmers.co.kr/learn/courses/30/lessons/17682


```java
// 내소스
class Solution {
    public static int solution(String dartResult) {
       int answer = 0;

    	Dart[] dart = new Dart[4];
    	Dart tmp = new Dart();
    	int i = 0;
    	for(String d:dartResult.split("")) {
    		if(Character.isDigit(d.charAt(0))) {
    			if(tmp.isFinData()) {
                    System.out.println(i);
    				dart[i++] = new Dart(tmp);
    				tmp.init();    				
    			}
    			tmp.addJumsu(d);
    		}
    		else {
    			if(d.compareTo("S") == 0 || d.compareTo("D") == 0 || d.compareTo("T") == 0)
    				tmp.setDoubleJumsu(d);
    			else if(d.compareTo("*") == 0)
    				tmp.setStar(2);
    			else if(d.compareTo("#") == 0)
    				tmp.setMinus(-1);
    		}
    	} 
                    System.out.println(i);
    	dart[i] = new Dart(tmp);
    	
    	for(int j=2;j>=0;j--) {
    		answer += (dart[j].getJumsu() * (j<2?dart[j+1].getStar():1));
    	}
    	
        
        return answer;
    }
}

class Dart {
	String jumsu = "";
	String d = "";
	int star = 1;
	int m = 1;
	
	public int getStar() {
		return star;
	}
	
	public boolean isFinData() {
		if(d.length()>0) return true;
		return false;
	}
	
	public void addJumsu(String str) {
		jumsu += str;
	}
	
	public void setDoubleJumsu(String str) {
		d = str;
	}
	
	public void setStar(int star) {
		this.star = star;
	}
	
	public void setMinus(int m) {
		this.m = m;
	}	
	
	public void init() {
		jumsu = "";
		d = "";
		star = 1;
		m = 1;
	}
	
	public int getJumsu() {
		int doubleScore = 1;
		if(d.compareTo("D") == 0) doubleScore = 2;
		else if(d.compareTo("T") ==0) doubleScore = 3;
		
		int score = Integer.parseInt(jumsu);
		return (int)Math.pow(score, doubleScore) * star * m;
	}
	Dart() {
		init();
	}
	Dart(Dart dart) {
		this.jumsu = dart.jumsu;
		this.d = dart.d;
		this.star = dart.star;
		this.m = dart.m;
	}
}
```



* 같은 숫자는 싫어
+ https://programmers.co.kr/learn/courses/30/lessons/12906

```java
import java.util.Arrays;
import java.util.Stack;

//프로그래머스 Level 1,같은 숫자는 싫어
public class EqualNumberNo {
    public int[] solution(int []arr) {
        Stack<Integer> stack = new Stack<>();
        
        for(int i=0;i<arr.length-1;i++) {
            if(arr[i] != arr[i+1])
                stack.push(arr[i]);
        }
        stack.push(arr[arr.length-1]);        
        return Arrays.stream(stack.toArray(new Integer[stack.size()])).mapToInt(Integer::intValue).toArray();
    }
}
```

   
***
   

* 나누어 떨어지는 숫자 배열
+ https://programmers.co.kr/learn/courses/30/lessons/12910?language

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class DivideNumberArray {
    public int[] solution(int[] arr, int divisor) {
        int[] answer = {-1};
        List<Integer> list = new ArrayList<Integer>();
        for(int d:arr) {
            if(d%divisor == 0) {
                list.add(d);
            }                
        }        
        
        if(list.size() == 0) return answer;
        answer = list.stream().mapToInt(Integer::intValue).toArray();
        Arrays.sort(answer);
        return answer;
    }
}

```


   
***
***
   

* 두 정수 사이의 합
+ https://programmers.co.kr/learn/courses/30/lessons/12912?language=javascript

```java
public class TwoNumberSum {
    public long solution(int a, int b) {
        return (a+b)*(Math.abs(a-b)+1)/2;
    }
}

```





* 문자열 내 마음대로 정렬하기
+ https://programmers.co.kr/learn/courses/30/lessons/12915?language=java


+ 내소스
```java
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

class SortCompare  implements Comparator<String> {
    public int idx;
    SortCompare(int i) { idx = i; }
    public int compare(String a, String b) {
        if(a.charAt(idx) == b.charAt(idx)) {
            return a.compareTo(b);
        }
        return Integer.compare(a.charAt(idx),b.charAt(idx));
    }
}


class Solution {
    public String[] solution(String[] strings, int n) {
        List<String> list = Arrays.asList(strings);
        Collections.sort(list, new SortCompare(n));
        return list.toArray(new String[list.size()]);
    }
}
```




* 문자열 내 p와 y의 개수
+ https://programmers.co.kr/learn/courses/30/lessons/12916?language=java


+ 내소스
```java
class Solution {
    boolean solution(String s) {
        if( s.replaceAll("[^pP]","").length() == s.replaceAll("[^yY]","").length() ) return true;
        return false;
    }
}
```




* 문자열 내림차순으로 배치하기
+ https://programmers.co.kr/learn/courses/30/lessons/12917?language=java


+ 내소스
```java
class Solution {
    public String solution(String s) {
        String[] array = s.split("");
        Arrays.sort(array,Collections.reverseOrder());
        return String.join("",array);
    }	
}
```

+ 다른사람소스(준규님)
```java
class Solution {
  public String solution(String s) {
    int[] numbers = s
      .chars()
      .map(i -> -i)
      .sorted()
      .map(i -> -i)
      .toArray();
    return new String(numbers, 0, numbers.length);
  }	
}
```













