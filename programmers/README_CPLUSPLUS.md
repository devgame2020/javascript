

* 문자열 다루기 기본
+ https://programmers.co.kr/learn/courses/30/lessons/12918

+ 내소스
```C++
#include <string>
#include <vector>

using namespace std;

bool solution(string s) {
    if(s.size() != 4 && s.size() != 6) return false;
    for(int i=0;i<s.size();i++)
        if(s[i] < '0' || s[i] > '9') return false;
    return true;
}
```



* 서울에서 김서방 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/12919

+ 내소스
```C++
#include <iostream>
#include <algorithm>
#include <string>
#include <vector>

using namespace std;

string solution(vector<string> seoul) {
    char str[128];
    vector<string>::iterator it = find(seoul.begin(), seoul.end(), "Kim");
    sprintf(str,"김서방은 %d에 있다", (it - seoul.begin()));
    string answer = str;
    return answer;
}
```




* 소수 찾기
+ https://programmers.co.kr/learn/courses/30/lessons/12921

+ 내소스
```C++
#include <string>
#include <vector>

using namespace std;

int solution(int n) {
    int answer = 0;
    int* arr = new int[n+1];
    for(int i=2;i<=n;i++) {
        if(arr[i]==2) continue;
        arr[i] = 1;
        for(int j=i*2;j<=n;j+=i) {
            arr[j] = 2;
        }
    }
    for(int i=2;i<=n;i++) 
        if(arr[i] == 1) answer++;
    delete[] arr;
    return answer;
}
```
