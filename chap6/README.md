# CSS 기초


+ style태그안에 css를 넣을수있다.
    + .js ==> 클래스 , #first ==> id
    + 클래스사용법
        + .js { font-weight: bold; }
        + 이렇게 css를 선언하고, 아래와 같이 사용이 가능하다.
        + <span class="js">내용</span>
    + id사용법    
        + #first { color:green; }
        + <span id="first" class="js">내용</span>
    + id는 식별하는것이고, 클래스는 그룹핑하는것임. id는 오직 1개만 존재해야함
    + span { color:blue; }  ==> html의 모든 span태그에 적용됨.
    + 정리하면 id가 우선순위가 제일 높고, 그다음에 클래스, 그 다음에 태그임
