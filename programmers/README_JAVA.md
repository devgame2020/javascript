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



* 문자열 다루기 기본
+ https://programmers.co.kr/learn/courses/30/lessons/12918?language=java

+ 내소스
```java
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
+ https://programmers.co.kr/learn/courses/30/lessons/12919?language=java

+ 내소스
```java
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

class Solution {
    public String solution(String[] seoul) {
        List<String> alist = Arrays.asList(seoul);
        return String.format("김서방은 %d에 있다",alist.indexOf("Kim"));
    }
}
```




* 소수 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/12921?language=java

+ 내소스
```java
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

class Solution {
    public int solution(int n) {
        int[] arr = new int[n+1];
        for(int i=2;i<=n;i++) {
            if(arr[i] == 2) continue;
            arr[i] = 1;
            for(int j=i*2;j<=n;j+=i) arr[j] = 2;
        }
        int sum = Arrays.stream(arr).reduce( 0,(x,y) -> {
            return x + (y==1?1:0);
        } );
        return sum;
    }
}
```




* 수박수박수박수박수박수?
+ https://programmers.co.kr/learn/courses/30/lessons/12922

```java
// 내소스
class Solution {
    public String solution(int n) {
        StringBuffer str = new StringBuffer(n);
        for(int i=0;i<n;i++) 
            str.append(i%2==0 ? "수" : "박");
        return str.toString();
    }
}
```







* 문자열을 정수로 바꾸기
+ https://programmers.co.kr/learn/courses/30/lessons/12925?language=java

```java
// 내소스
class Solution {
    public int solution(String s) {
        return Integer.parseInt(s);
    }
}
```




* 시저 암호
+ https://programmers.co.kr/learn/courses/30/lessons/12926?language=java

```java
// 내소스
class Solution {
    public String solution(String s, int n) {
        int base = 65;
        StringBuffer str = new StringBuffer(n);
        for(int i=0;i<s.length();i++) {
            int x = (int)s.charAt(i);
            if(x == 32) {
                str.append(' ');
            }
            else {
                base = x<=90?65:97;
                str.append(Character.toString(base + (x+n-base)%26));
            }
        }
        return str.toString();
    }
}
```



* 정수 내림차순으로 배치하기
+ https://programmers.co.kr/learn/courses/30/lessons/12933?language=java

```java
// 내소스
import java.util.Arrays;

class Solution {
    public long solution(long n) {
        long answer = 0;        
        StringBuffer str = new StringBuffer();
        String str2 = String.valueOf(n);
        char[] arr = str2.toCharArray();
        Arrays.sort(arr);
        for(int i=arr.length-1;i>=0;i--) 
        	str.append(arr[i]);    
        return Long.parseLong(str.toString());
    }
}

```


* 정수 제곱근 판별
+ https://programmers.co.kr/learn/courses/30/lessons/12934?language=java

```java
// 내소스
class Solution {
    public long solution(long n) {
        long answer = (long)Math.sqrt((double)n);
        if(Math.pow((double)answer, 2) == n) return (long)Math.pow((double)(answer+1), 2);
        return -1;
    }
}

```


* 제일 작은 수 제거하기
+ https://programmers.co.kr/learn/courses/30/lessons/12935?language=java

```java
// 내소스
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int[] solution(int[] arr) {        
        int[] answer = {-1};
    	if(arr.length <= 1) return answer;

        answer = new int[arr.length-1];
    	int min = arr[0];
    	for(int d:arr) if(min>d) min = d;
        for(int i=0,j=0;i<arr.length;i++,j++) {            
            if(min==arr[i]) { j--; continue; }
            answer[j] = arr[i];
        }
        return answer;
    }
}
```

* 짝수와 홀수
+ https://programmers.co.kr/learn/courses/30/lessons/12937?language=java

```java
// 내소스
class Solution {
    public String solution(int num) {
        return num % 2 == 0 ? "Even" : "Odd";
    }
}
```




* 최대공약수와 최소공배수
+ https://programmers.co.kr/learn/courses/30/lessons/12940?language=java

```java
// 내소스
public class Solution  {
    public int[] solution(int n, int m) {
        int[] answer = { 0,0 };
        answer[1] = n*m;
        
        int mod=0;
        while(true) {
            mod = n%m;
            if(mod==0) {
                answer[0] = m;
                break;   
            }
            n = m;
            m = mod;
        }
        answer[1] /= answer[0];
        return answer;
    }
}
```



* 콜라츠 추측
+ https://programmers.co.kr/learn/courses/30/lessons/12943?language=java

```java
// 내소스
class Solution {
    public int solution(int num) {
        if(num==1) return 0;
        long x = num;
        for(int i=1;i<=500;i++) {
            x = x%2==0 ? x/2 : (x*3+1);
            if(x==1) return i;
        }
        return -1;
    }
}
```



* 평균 구하기
+ https://programmers.co.kr/learn/courses/30/lessons/12944?language=java

```java
// 내소스
import java.util.Arrays;

class Solution {
    public double solution(int[] arr) {
        return (double)Arrays.stream(arr).sum() / arr.length;
    }
}
```



* 하샤드 수
+ https://programmers.co.kr/learn/courses/30/lessons/12947?language=java

```java
// 내소스
class Solution {
    public int digit_sum(int x) {
        if(x<1) return x;
        return x%10 + digit_sum(x/10);
    }
    
    public boolean solution(int x) {
        if(x%digit_sum(x) == 0) return true;
        return false;
    }
}
```






* 핸드폰 번호 가리기
+ https://programmers.co.kr/learn/courses/30/lessons/12948?language=java

```java
// 내소스
class Solution {
    public String solution(String phone_number) {
        return "*".repeat(phone_number.length()-4) + phone_number.substring(phone_number.length()-4);
    }
}
```




* 행렬의 덧셈
+ https://programmers.co.kr/learn/courses/30/lessons/12950

```java
// 내소스
import java.util.Arrays;

class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = Arrays.copyOf(arr1, arr1.length);
        for(int i=0;i<answer.length;i++) {
        	for(int j=0;j<answer[i].length;j++)
        		answer[i][j] += arr2[i][j];
        }
        return answer;
    }
}
```




* x만큼 간격이 있는 n개의 숫자
+ https://programmers.co.kr/learn/courses/30/lessons/12954

```java
// 내소스
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = new long[n];
        for(int i=1;i<=n;i++)
            answer[i-1] = (long)x*(long)i;
        return answer;
    }
}
```




* 직사각형 별찍기
+ https://programmers.co.kr/learn/courses/30/lessons/12969

```java
// 내소스
import java.util.Scanner;

class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();

        String str = "*".repeat(a) + "\n";
        System.out.println(str.repeat(b));
    }
}
```




* 신고 결과 받기
+ https://programmers.co.kr/learn/courses/30/lessons/92334

```java
// 내소스
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        int[] answer = new int[id_list.length];
        int[] block_list = new int[id_list.length];
        int[] ucnt = new int[id_list.length];
        int[] idx_list = new int[id_list.length];
        
        // report의 중복값 제거
        Set<String> report2 = new HashSet<>();
        for(String d:report) {
        	report2.add(d);
        }
        
        // 빠른 검색을 위하여 id_list정렬
        String[] id_list2 = Arrays.copyOf(id_list, id_list.length);
        Arrays.sort(id_list2);
        
        // 정렬된 유저와 정렬안된 유저를 매칭하기 위한 인덱스List
        for(int i=0;i<id_list.length;i++) {
        	String d = id_list[i];
        	idx_list[i] = Arrays.binarySearch(id_list2, d);
        }
        
        // 신고당한 유저카운트 (각각의 유저가 몇번 신고당했는지카운트값 저장) 
        for(String d:report2) {
        	String[] tmp = d.split(" ");
        	int index2 = Arrays.binarySearch(id_list2, tmp[1]);
        	ucnt[index2]++;
        }
        
        // 신고한 유저들의 각각의 블럭당한 유저 카운트
        for(String d:report2) {
        	String[] tmp = d.split(" ");
        	int index = Arrays.binarySearch(id_list2, tmp[0]);
        	int index2 = Arrays.binarySearch(id_list2, tmp[1]);
        	if(ucnt[index2]>=k) block_list[index]++;
        }
               
        for(int i=0;i<id_list.length;i++) {
        	answer[i] = block_list[idx_list[i]];
        }               
        
        return answer;
    }
}
```














   
***
***
   
* Level 2

   
***
***
   




* n^2 배열 자르기
+ https://programmers.co.kr/learn/courses/30/lessons/87390?language=java

```java
// 내소스
class Solution {
    public int[] solution(int n, long left, long right) {
        int[] answer = new int[(int)right-(int)left+1];

        long idx = 0;
        int i = 0;
        for(long x=1;x<=n;x++) {
            if(idx>right) break;
            if(idx+n < left) {
                idx += n;
                continue;
            }
            for(long y=1;y<=n;y++) {
                long d = y<=x?x:y;            
                if(idx>=left && idx<=right) answer[i++] = (int)d;
                idx++;
            }
        }

        return answer;
    }
}
```




* 멀쩡한 사각형
+ https://programmers.co.kr/learn/courses/30/lessons/62048?language=java

```java
// 내소스
class Solution {
    public int gcd(int w,int h) {
        int mod = w%h;
        if(mod==0) return h;
        return gcd(h,mod);
    }
    
    public long solution(int w, int h) {
        return (long)w*h - (w+h-gcd(w,h));
    }
}
```






* 124 나라의 숫자
+ https://programmers.co.kr/learn/courses/30/lessons/12899?language=java

```java
// 내소스
class Solution {
    public String solution(int n) {
        StringBuffer answer = new StringBuffer();
        while(n>0) {
            int mod = n%3;
            answer.append((mod==0?4:mod));
            n = n/3 - (mod==0?1:0);
        }
        return answer.reverse().toString();
    }
}
```




* 기능개발
+ https://programmers.co.kr/learn/courses/30/lessons/42586?language=java

```java
// 내소스
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        List<Integer> list = new ArrayList<Integer>();

        int d = (int)Math.ceil((100.0-progresses[0])/speeds[0]);
        int fin=1;
        for(int i=1;i<progresses.length;i++) {
            int ptime = (int)Math.ceil((100.0-progresses[i])/speeds[i]);
            if(d>=ptime) fin++;
            else {
                list.add(fin);
                fin=1;
                d = ptime;
            }
        }
        list.add(fin);
        
        return list.stream().mapToInt(Integer::intValue).toArray();
    }
}
```



* 타겟 넘버
+ https://programmers.co.kr/learn/courses/30/lessons/43165

```java
// 내소스
import java.util.Arrays;

class Solution {
	public static int recursive(int[] numbers,int target,int idx) {
        if(idx >= numbers.length) {
        	if(Arrays.stream(numbers).sum() == target) return 1;
            return 0;
        }
        
        int sum = 0;
        sum += recursive(numbers,target,idx+1);
        numbers[idx] *= -1;
        sum += recursive(numbers,target,idx+1);  
        return sum;
	}
    public int solution(int[] numbers, int target) {
        return recursive(numbers,target,0);
    }
}
```








