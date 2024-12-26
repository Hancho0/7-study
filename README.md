# 7주차 Study [ 2024-12-16 ~ 2024-12-20 ]

**[ 목표 ]**
- 이번주 목표 : 도큐먼트 파일 입출력 및 템플릿 , 사용자 인터페이스
-----

**[ 진행 사항 ]**

[ 도큐먼트 ]
도큐먼트의 주요 기능은 도큐먼트 데이터에 접근하기 위한 인터페이스를 제공하고 데이터를 저장하고 읽어오는 역할을 한다. 도큐먼트는 저장 매체와 뷰 사이의 매개 역할을 하고 뷰는 도큐먼트의 정보를 윈도우에 출력하는 역할을 한다.

1) CDocument 클래스<br>
데이터를 관리하는 클래스이다.<br>
프로그램이 사용하는 데이터를 만들고, 읽어오고, 저장하는 역할을 담당한다.

2) Carchive 클래스<br>
표쥰 C++ 라이브러리 iostream 클래스와 상당히 비슷하다.<br>
도큐먼트의 데이터를 읽고 쓰기 위한 삽입(<<) 및 추출(>>) 연산자를 정의하고 있다.<br>
이진 삽입(<<) 연산자는 데이터를 순차적으로 저장할 때 사용하며 이진 추출(>>) 연산자는 춘차적으로 데이터를 읽어 들일 때 사용한다.<br>
Carchive 클래스에서 "저장"의 의미는 메모리에 있는 데이터가 파일로 전송되는 것을 말하고, "열기"의 의미는 파일에 있는 데이터가 메모리로 전송되는 것을 의미한다.

3) Serialize() 함수<br>
직렬화란 하드디스크와 같은 저장 매체에 데이터를 저장하고 읽어 들이는 과정을 말한다.<br>
직렬화의 기본적인 기능은 CObject 클래스의 Serialize() 함수에 정의되어 있다.<br>
MFC에서는 도큐먼트 클래스가 자기 자신의 데이터를 관리하므로 도큐먼트 클래스에서 Serialize() 함수를 오버라이딩 하면 된다.

[ 실습 1 ]
https://github.com/Hancho0/7-study/blob/main/README2.md

[ 실습 2 ]
https://github.com/Hancho0/7-study/blob/main/README3.md

[ 사용자 인터페이스 ]

* 풀 다운 메뉴(Pull-down Menu)<br>
애플리케이션 상단에 여러 개의 카테고리가 일렬로 늘어서 있는 형태를 취하고 있으며, 사용자가 카테고리 하나를 선택하면 선택된 카테고리 아래로 메뉴가 뚝 떨어지면서 애플리케이션의 기능을 작동시킬 수 있는 메뉴 항목이 나타난다.

* 캐스케이딩 메뉴(Cascading Menu)<br>
다운 메뉴에서 변형된 메뉴 형태로, 메뉴 항목의 오른쪽에 또 하나의 서브 메뉴가 나타나는 메뉴이다.

* 팝엄 메뉴(Pop-up Menu) 또는 문맥 메뉴(Context Menu)<br>
애플리케이션 영역의 중간에서 자유롭게 튀어나오는 메뉴이다. 커서나 마우스 포인터로 선택된 객체 혹은 작업 영역에 따라 다른 팝업 메뉴를 띄울 수 있다.

-----
**[ 이번 Study를 통해 느낀점 ]**

이사 하느라 사용자 인터페이스 실습한 내용을 github에 정리하진 못했습니다. 도큐먼트 파일 입출력 및 템플릿 파트 하면서 데이터 입력 출력 하면서 불러오기 를 좀더 집중적으로 배울 수 있었던거 같습니다. 프로젝트 진행하면서 본체에서는 Combo Box에 데이터를 입력하고 나서 출력해보면 한글이 깨지는 오류를 발견해서 utf-8 등 여러가지 수정을 해보았으나 안되서 노트북으로 하니까 데이터가 한글이 안깨지고 정상적으로 출력되는 문제를 직면했습니다. 그래서 이 부분을 어떻게 해결할지 좀더 공부 해야할거 같다는 생각이 들었던 파트였던거 같습니다. 다른 부분에선 한글이 안깨지는데 Combo Box에 데이터를 입력하기만 하면 깨져서 문제를 어떻게 해결할지 고민되는거 같습니다. 다음주에는 네트워크도 함께 공부하면서 각종 프로젝트 진행했던거 복습하는 과정을 거쳐 입사 후 좀더 실무에서 어떻게 도움될지, 언어에 대해 좀더 깊게 공부하는 시간을 가질거 같습니다.
