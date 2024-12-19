# 실습 2

-------

프로젝트 이름을 "MDI" 라고 정한다.

애플리케이션 종류 단게 에서 "여러문서"를 선택
그리고 [문서 템플릿 속성] 에서 [파일 확장명] 항목에서 txt를 입력한다.
그리고 [생성된 클래스] 단게에서 [생성된 클래스] 항목을 ChildFarame 으로 지정하고 프로젝트를 생성한다

[리소스 뷰] 에서 Dialog 에서 삽입해서 새로운 대화상자 폼을 생성한다.

[ID] 를 IDD_DIALOG_CARD 로 설정하고 [캡션]은 "문자열 및 위치 입력으로 설정한다.

그리고 나서 [도구 상자] 에서 Static Text 와 Edit Control 선택하여 다음과 같이 배치한다.

![스크린샷 2024-12-18 222621](https://github.com/user-attachments/assets/aad4817d-2b3c-43b8-b859-f029d020fe8a)

그리고 나서 각각 [캡션] 을 "X :","Y :","문자열 :" 라고 입력후
[ID]를 각각 IDC_EDIT_X, IDC_EDIT_Y, IDC_EDIT_TEXT 라고 입력한다.

그리고 나서 [MFC 클래스 추가]를 통해 클래스 이름은 CInputDIg 로 하고나서
[클래스 마법사]를 실행시켜 [멤버 변수] 란에서 IDC_EDIT_TEXT 를 선택후 변수를 추가한다.
[범주]는 "값" [이름]은 "m_strText" [변수 형식] 은 CString 으로 지정한다.

위와 같은 방법으로 IDC_EDIT_X 를 선택 후
[범주]는 "값" [이름]은 "m_nX" [변수 형식] 은 int 으로 지정한다.

똑같이 IDC_EDIT_Y 를 선택 후
[범주]는 "값" [이름]은 "m_nY" [변수 형식] 은 int 으로 지정한다.

그리고 나서 문자열을 출력할 위치를 저장하는 멤버 변수를 초기화 하기 위해
[클래스 뷰]에서 CInputDIg 클래스의 생성자 함수인 CInputDIg 함수 본체로 이동 후 다음과 같이 코드를 입력한다.

```ruby
CInputDIg::CInputDIg(CWnd* pParent /*=nullptr*/)
	: CDialogEx(IDD_DIALOG_INPUT, pParent)
	, m_strText(_T(""))
	, m_nX(0)
	, m_nY(0)
{
	m_nX = 30;
	m_nY = 30;
}
```

그리고 나서 CMDIDoc 클래스에 문자열과 위치 정보를 저장할 3개의 멤버 변수를 추가한다.
[클래스 뷰] 에서 CMDIDoc 클래스를 선택하고 [변수 추가]한다.

| 변수 형식 | 변수 이름 | 용도 |
|---|---|---|
| int | m_nDocX | X 좌표를 저장하기 위한 변수 |
| int | m_nDocY | Y 좌표를 저장하기 위한 변수 |
| CString | m_strDocText | 문자열을 저장하기 위한 변수 |

그리고 나서 [클래스 마법사]를 실행한후 [클래스 이름] 항목에서 CMDIView 를 선택하고 [메시지] 항목에서 WM_RBUTTONDOWN을 선택하여 함수를 생성한다.

그리고 나서 다음과 같은 코드를 작성한다.

```ruby
void CMDIView::OnRButtonDown(UINT nFlags, CPoint point)
{
	// TODO: 여기에 메시지 처리기 코드를 추가 및/또는 기본값을 호출합니다.
	CInputDIg* pInput = new CInputDIg; //대화상자 객체 생성
	if (pInput->DoModal() == IDOK) //DoModal()함수는 대화상자를 실행시킨다.
	{

  }
	CView::OnRButtonDown(nFlags, point);
}
```

그리고 나서 CMDIView 클래스에 CInputDIg 클래스의 정보가 없으므로 CInputDIg 클래스를 참조하기 위해 "CInputDIg.h" 파일을 include 한다.

```ruby
#include "CInputDIg.h"
```

그리고 나서 다음과 같은 코드를 추가로 작성한다.

```ruby
void CMDIView::OnRButtonDown(UINT nFlags, CPoint point)
{
	// TODO: 여기에 메시지 처리기 코드를 추가 및/또는 기본값을 호출합니다.
	CInputDIg* pInput = new CInputDIg; //대화상자 객체 생성
	if (pInput->DoModal() == IDOK) //DoModal()함수는 대화상자를 실행시킨다.
	{
		CMainFrame* pFrame = (CMainFrame*)AfxGetMainWnd();
		CChildFrame* pChild = (CChildFrame*)pFrame->GetActiveFrame();
		CMDIDoc* pDoc = (CMDIDoc*)pChild->GetActiveDocument();

		UpdateData(TRUE); //데이터를 변수에 저장
		//도큐먼트 클래스의 멤버 변수에 입력된 값을 저장
		pDoc->m_nDocX = pInput->m_nX;
		pDoc->m_nDocY = pInput->m_nY;
		pDoc->m_strDocText = pInput->m_strText;
		Invalidate(); //화면 갱신
	}
	CView::OnRButtonDown(nFlags, point);
}
```

그리고 CMainFrame 클래스와 CChildFrame 클래스에 대한 정보가 없으므로 헤더파일을 include 시킨다.

```ruby
#include "MainFrm.h"
#include "ChildFrm.h"
```

그리고 나서 CMDIView 클래스의 OnDraw 함수에 다음 코드를 추가한다.

```ruby
void CMDIView::OnDraw(CDC* pDC) //주석해제
{
	CMDIDoc* pDoc = GetDocument();
	ASSERT_VALID(pDoc);
	if (!pDoc)
		return;

	// TODO: 여기에 원시 데이터에 대한 그리기 코드를 추가합니다.
	pDC->TextOut(pDoc->m_nDocX, pDoc->m_nDocY, pDoc->m_strDocText);
}
```

[ 출력 결과 ]

![스크린샷 2024-12-19 184921](https://github.com/user-attachments/assets/e581d2c6-649b-4671-84f4-7b8b3af0d3a6)
![스크린샷 2024-12-19 184929](https://github.com/user-attachments/assets/6a73b105-efd2-4aba-b5bb-2072c7990c4e)
![스크린샷 2024-12-19 185001](https://github.com/user-attachments/assets/2e8fe0d9-a03c-4a96-a4a2-892e794cfbfc)
![스크린샷 2024-12-19 185010](https://github.com/user-attachments/assets/9435c200-559b-46c0-9d9d-6e361b5f18ed)
![스크린샷 2024-12-19 185019](https://github.com/user-attachments/assets/72b5fae1-67b5-4ce8-9877-1f88898483fc)
