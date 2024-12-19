# 실습 1

-------

[리소스 뷰]의 Dialog 에서 삽입을 해서 새로운 대화상자 폼 하나 생성한다.<br>
그리고 나서 ID 는 IDD_DIALOG_CARD 캡션은 "학생 카드 작성" 으로 설정 하고<br>
도구상자에서 Static Text, Edit Control, Combo box, Radio Button, Check Box 선택하여 다음과 같이 배치한다.<br>

![스크린샷 2024-12-18 214910](https://github.com/user-attachments/assets/1fd6a1f9-89bb-4772-8e3c-f7363d2da9d9)

Staitc Text 컨트롤에 캡션을 각각 "학 과 :","이 름 :","성 별 :","취 미 :" 라고 입력한다.

그리고 나서 Combo Box는 ID를 IDC_COMBO_DEPT 로 설정하고<br>
데이터에 "경영학과;간호학과;컴퓨터공학과;한의학과;전자공학과;일어일문학과"로 입력한다.<br>
정렬을 false로 하고 형식을 Drop List로 한다.<br>

그리고 나서 Edit Control 속성에 ID는 IDC_EDIT_NAME으로 설정한다.

그리고 나서 첫번째 Radio Button 컨트롤에 ID를 IDC_RADIO_MALE로 설정하고 캡션을 "남자"로 지정한다.<br>
두번째 Radio Button 컨트롤에 ID를 IDC_RADIO_FEMALE로 설정하고 캡션을 "여자"로 지정한다.

그리고 첫번째 Check Box 에서 ID는 IDC_CHECK_READING 으로 지정하고 캡션을 "독서" 으로 지정한다.<br>
두번째 Check Box 에서 ID는 IDC_CHECK_SPORTS 으로 지정하고 캡션을 "운동" 으로 지정한다.<br>
세번째 Check Box 에서 ID는 IDC_CHECK_FISHING 으로 지정하고 캡션을 "낚시" 으로 지정한다.

그러면 다음과 같은 폼이 만들어진다.

![스크린샷 2024-12-19 135404](https://github.com/user-attachments/assets/731f42a2-e324-4bcd-b056-8891036022d5)

그리고 나서 MFC 클래스 추가를 해서 클래스 이름은 "CCardDIg"로 하고 확인한다.

클래스 마법사를 실행하고 [멤버 변수]탭에서 [컨트롤 ID] 항목은 IDC_COMBO_DEPT로 선택하고 변수 추가한다.
[제어 변수 추가] 에서 [범주]는 "값"을 선택하고 [이름] 항목은 m_strDept라고 입력한 후 [변수 형식]은 CString으로 설정한다.

그리고 IDC_EDIT_NAME 항목에서도 [범주]는 "값"을 선택하고 [이름] 항목은 m_strName라고 입력한 후 [변수 형식]은 CString으로 설정한다.

그리고 나서 클래스 마법사에서 [클래스 이름] 항목에 CStudyCardView을 선택하고 [메시지] 항목은 WM_RBUTTONDOWN을 선택하여 추가하고 다음과 같은 코드를 작성한다.

```ruby
void CStudyCardView::OnRButtonDown(UINT nFlags, CPoint point)
{
	// TODO: 여기에 메시지 처리기 코드를 추가 및/또는 기본값을 호출합니다.
	CCardDIg* pCard = new CCardDIg; //대화상자 객체 생성
  if(pCard->DoModal() == IDOK)
  {

  }
  CView::OnRButtonDown(nFlags, point);
}
```

CStudyCardView 클래스에서 CCardDIg 클래스의 정보가 없으므로 클래스를 참조하기 위해 "CCardDIg.h" 파일을 include를 시킨다

```ruby
#include "CCardDIg.h"
```

클래스 마법사에서 [클래스 이름]을 CCardDIg [명령] 탭에서 [개체 ID] 항목은 IDC_RADIO_MALE을, [메시지] 항목은 COMMAND를 선택하고 추가하여 다음과 같은 코드를 작성한다.

```ruby
void CCardDIg::OnRadioMale()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	m_bSex = TRUE;
}
```

그리고 Female도 똑같이 하여 다음 코드 작성한다.

```ruby
void CCardDIg::OnRadioFemale()
{
	// TODO: 여기에 명령 처리기 코드를 추가합니다.
	m_bSex = FALSE;
}
```

그리고 나서 IDC_CHECK_READING 항목에서 BN_CLICKED 를 선택하고 다음과 같은 코드를 작성한다.

```ruby
void CCardDIg::OnClickedCheckReading()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	m_bHobby[0] = !m_bHobby[0];
}
```

그리고 똑같이 IDC_CHECK_SPORTS 에도 똑같이 다음과 같은 코드를 작성한다.

```ruby
void CCardDIg::OnClickedCheckSports()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	m_bHobby[1] = !m_bHobby[1];
}
```

그리고 똑같이 IDC_CHECK_FISHING 에도 똑같이 다음과 같은 코드를 작성한다.

```ruby
void CCardDIg::OnClickedCheckFishing()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	m_bHobby[2] = !m_bHobby[2];
}
```

그리고 나서 CStudyCardView 클래스에서 학생 정보 저장에 필요한 4개의 멤버 변수를 추가한다.

| 변수 형식 | 변수 이름 | 용도 |
|---|---|---|
| CString | m_strDept | 학과을 저장하기 위한 변수 |
| CString | m_strName | 
