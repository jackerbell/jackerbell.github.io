---
categories: Coding
tag: C++
toc: true
author_profile: false
---

# 2023. 08. 17. MFC 프로젝트 Pocker! 정리

## 요구사항 
1. 5개의 중복되지 않는 난수를 발생시키고 해당하는 카드를 보여줍니다.
2. 포커 족보에서 어떤 것에 해당하는지 분석하여 출력 (ex 모두 무늬가 같으면 플러시..)
3. 전체 족보를 조회할 수 있는 화면을 넣을 것
4. 자유 추가 기능 구현(ex 10000번 수행 후 족보의 확률 분석...)
5. 수행 기록을 txt 파일로 저장
6. UI에서 파일을 불러와 수행 기록을 조회

<br>
<br>

## 요구사항 분석
* 5개의 **중복되지 않는 난수** 발생 & 카드 이미지 출력
  * 요구사항에 맞는 CTRL → Picture Ctrl
  * 난수 발생 → rand(), srand((int)time(NULL))

<br>

* 포커 족보 로직 분석 및 버튼의 캡션 변경!
  *  포커 규칙 파악을 통한 로직 분석
  *  버튼 이벤트를 통한 Edit Ctrl의 캡션 변경

<br>

*  많은 양의 이미지 및 텍스트를 사용자에게 보여 주어야함
  * 페이지에 스크롤 기능 첨부 or 탭 기능 활용

<br>

* 자유 기능 추가 구현
  * 메인 화면과 다른 다이얼로그 창에서 edit ctrl에 입력한 횟수만큼 포커 로직을 반복 수행해야 함
  * 포커 로직의 경우 따로 메서드로 만들어서 사용
  * 입력 받는 Edit ctrl의 값을 문자열(CString)에서 정수형(int)로 변환.
  * 시뮬레이터 작동 후 각 족보 text 옆에 있는 edit ctrl에 시행결과 등장한 각 족보의 확률을 표시해야함. 
    → 각 족보별로 count할 정수형 변수선언, 입력한 count와 확률 계산 및 시행횟수도 별도로 표시해야하므로 문자열 변환
    → 메인 화면에서 만들었던 메서드를 다소 변경할 필요가 있음 (return vector<CString> → return vector<int>)

<br>

* 수행 기록을 txt 파일로 저장
  * 파일 입출력 클래스 파악 (CStdio, CFile...)

<br>

* UI에서 파일을 열기 → 외부 파일 열기
  * 외부 실행 프로그램 실행(ShellExecute) 

## 문제 해결
* 5개의 **중복되지 않는 난수** 발생 & 카드 이미지 출력
```cpp
// in PockerDlg.cpp 
int temp = 0;
vector<int> index = { rand() % 52,rand() % 52, rand() % 52, rand() % 52, rand() % 52 }; // 버튼 이벤트 시 랜덤 인덱스 부여
srand((int)time(NULL));
for (int i = 0; i < 5; i++) // 중복 방지 로직
{
  
  temp = index[i];
  for (int j = 0; j < i; j++)
  {
    if (temp == index[j]) 
    {
      index[i] = rand() % 52;
      i--;
    }
  }
}
```

위의 코드를 작성할 때, 주의할 점은 srand((int)time(NULL));을 작성한다고 생성된 난수들이 무조건 중복이 방지되지는 않는다! <br>
반드시 아래의 반복문처럼 중복시 난수를 다시 생성하는 로직을 작성해야한다! <br>
그리고 srand의 동작원리 및 반복문의 동작시간을 깜빡해 뒤에서 만들 포커 반복 로직에서 난수가 고정된 상태로 반복된 **참사**를 겪었다. <br>
핵심은 반복문의 동작시간이 srand에 넣은 time의 동작시간(1s)보다 매우 짧기 때문에 난수가 고정되어버려서 계속 똑같은 난수로 고정되어버린것!!! <br>
이런 단순한 실수 하나때문에 엄청 시간을 놓쳐버렸다. ㅠㅠ <br>

<br>

카드 이미지의 경우 처음에는 다소 이상한 방법으로 생성했었는데, <br>
북마크에 표시해두지 않아서 기록을 다시 찾아봐야한다;; 앞서 시도했던 방법은 다음 기회에 분석을 ... <br>
CImage 클래스를 사용해서 이미지를 띄워보았고 아래는 참조했던 사이트이다.
<a href="https://garage-fullof-dummy.tistory.com/68">MFC 픽쳐컨트롤</a> <br>
<br>

다이얼로그 초기화면을 기준으로 이벤트없이 이미지만 띄우려고 했으나,  참조한 자료가 이벤트를 활용한 방법이라 이번엔 이벤트로 대체했다. <br>
방법을 요약하면 아래와 같다. <br><br>
1. 생성한 Picture Ctrl의 ID를 변경, IDC_STATIC(Default) → IDC_PIC~ <br>
![캡처](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/3b661677-850b-4271-9bad-035d90c03847) <br><br>
2. Picture Ctrl의 각 타입을 Frame으로 변경 <br>
![1](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/94366545-4a55-4224-b845-4bdc744d80c5) <br><br>
3. Button 이벤트용 Btn ctrl의 생성 및 click 이벤트 생성 <br>
![2](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/add7ef2e-c87b-4c59-beae-6aeffa39da7c) <br><br>
4. Picture Ctrl의 변수 생성 (control 범주) <br>
![1](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/0a97bd33-e0f8-4724-b326-034e658fab37) <br><br>
5. Button 이벤트 동작을 위해 아래와 같이 코드 작성
```cpp
void CPockerDlg::OnClickedButtonPocker()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	CRect rect;	//픽쳐 컨트롤의 크기를 저장할 CRect 객체
	CDC* dc1; //픽쳐 컨트롤의 DC를 가져올  CDC 포인터 여기서 dc는 GDI(화면에 글을 쓰거나 그림 넣는 행동들 담당)을 의미.. 
	CDC* dc2; 
	CDC* dc3; 
	CDC* dc4; 
	CDC* dc5; 

	CImage image1;	//불러오고 싶은 이미지를 로드할 Cimage 클래스 변수들을 통해 불러옴.. 
	CImage image2;	
	CImage image3;	
	CImage image4;	
	CImage image5;	

	m_pic_ctrl1.GetWindowRect(rect);  //GetWindowRect를 사용해서 픽쳐 컨트롤의 크기를 받는다.
	m_pic_ctrl2.GetWindowRect(rect);  
	m_pic_ctrl3.GetWindowRect(rect);  
	m_pic_ctrl4.GetWindowRect(rect);  
	m_pic_ctrl5.GetWindowRect(rect);  

	dc1 = m_pic_ctrl1.GetDC();	//픽쳐 컨트롤의 DC(일종의 제어권?)를 얻는다.
	dc2 = m_pic_ctrl2.GetDC();	
	dc3 = m_pic_ctrl3.GetDC();	
	dc4 = m_pic_ctrl4.GetDC();	
	dc5 = m_pic_ctrl5.GetDC();	


	int temp = 0;
	vector<int> index = { rand() % 52,rand() % 52, rand() % 52, rand() % 52, rand() % 52 }; // 버튼 이벤트 시 랜덤 인덱스 부여
	srand((int)time(NULL));
	for (int i = 0; i < 5; i++) // 중복 방지 로직
	{
		
		temp = index[i];
		for (int j = 0; j < i; j++)
		{
			if (temp == index[j]) 
			{
				index[i] = rand() % 52;
				i--;
			}
		}
	}

	vector<CString> deck; // 뽑은 5장의 카드 경로를 저장하는 CString Vector
	CString pedigree;

	for (int i = 0; i < 5; i++) 
	{
		deck.push_back(Routes[index[i]]); // 순차적으로 deck에 삽입
	}

	sort(deck.begin(), deck.end()); // 오름차순 정렬 

	
	pedigree = DiscriPedigree(deck)[0];

	image1.Load(deck[0]);	//이미지 로드
	image2.Load(deck[1]);
	image3.Load(deck[2]);
	image4.Load(deck[3]);
	image5.Load(deck[4]);

	SetDlgItemText(IDC_BUTTON_POCKER, pedigree);


	image1.StretchBlt(dc1->m_hDC, 0, 0, rect.Width(), rect.Height(), SRCCOPY);	//이미지를 픽쳐 컨트롤 크기로 조정
	image2.StretchBlt(dc2->m_hDC, 0, 0, rect.Width(), rect.Height(), SRCCOPY);	
	image3.StretchBlt(dc3->m_hDC, 0, 0, rect.Width(), rect.Height(), SRCCOPY);	
	image4.StretchBlt(dc4->m_hDC, 0, 0, rect.Width(), rect.Height(), SRCCOPY);	
	image5.StretchBlt(dc5->m_hDC, 0, 0, rect.Width(), rect.Height(), SRCCOPY);	

	ReleaseDC(dc1);	//DC 해제
	ReleaseDC(dc2);	
	ReleaseDC(dc3);	
	ReleaseDC(dc4);	
	ReleaseDC(dc5);	
}
```

<br>

아래는 출력 결과! ↓ <br>

![3](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/ee3d023b-14d0-4e89-8ebc-6c4332843aba) <br><br><br>

* 포커 족보에서 어떤 것에 해당하는지 분석하여 출력 (ex 모두 무늬가 같으면 플러시..) <br>
처음엔 엄청 복잡해보여서 많이 힘들었는데 포커 사이트에 게시된 규칙들을 분석해보니 의외로 간단히 해결할 수 있었다. <br>
일단, 크게 조건을 두가지로 나누었다. <br>
다섯장의 카드의 무늬가 같은지 아닌지에 따라서 둘로 나누었다. <br>
플러쉬에 해당하는 족보들은 모든 카드의 무늬가 같아야한다는 공통 조건을 가지고 있으므로 로얄플러쉬, 스트레이트플러쉬, 플러쉬 이 세 가지를 우선 한 카테고리 안에 넣었다. <br><br>
그 외에 남은 부분들은 포카드, 풀하우스, 트리플, 투페어, 원페어, 스트레이트, 하이카드, 이렇게 7가지이다. <br>
위 족보들에도 공통점이 있다. <br>
그건 바로 카드의 종과 상관없이 같은 숫자의 개수에 따라 결정이 된다는 것! <br>
그래서 **동일한 숫자의 카드수**에 따라 우리는 족보를 판별할 수 있게 된다. <br>
동일한 숫자인지의 여부를 따지기 위해서는 문자열의 1~2 index까지 자를 필요성이 있었는데, 이 때, `Mid(start index, num)`를 활용하였다. <br>
그리고 `==` 연산자를 통해 둘의 동일여부를 따진 후 족보를 판별하는 로직을 만들었다. <br><br>
```cpp
vector<CString> CPockerDlg::DiscriPedigree(vector<CString> deck) // 5개의 카드 패가 담긴 deck 넘김 DiscriPedigree
{
	// TODO: 여기에 구현 코드 추가.
	vector<CString> pedigree;
	int isDiffShape = 0;
	int isSameNum = 0;

	for (int i = 0; i < 4; i++)
	{
		for (int j = i + 1; j < 5; j++)
		{
			if (deck[i].Mid(0, 1) != deck[j].Mid(0, 1)) // 동일한 문양인지 검증
			{
				isDiffShape++;
			}

		}
	}

	for (int i = 0; i < 4; i++)
	{
		for (int j = i + 1; j < 5; j++)  // 1 2 2 1 2 기대값 4... 1 + 3 = 4 같은 숫자 2쌍일 때 풀하우스   
		{								 // 1 2 3 3 4 기대값 1... 0 + 1 = 1 원페어
										 // 1 3 3 4 4 기대값 2... 1 + 1 = 2 투페어
										 // 1 2 2 2 3 기대값 3... 2 + 1 = 3 트리플
										 // 1 1 1 1 4 기대값 6... 3 2 1 = 6 .. 포카드 
										 // 1 2 3 4 5 기대값 0 .. max-min = 4 스트레이트
										 // 나머지 경우 하이카드 
			if (deck[i].Mid(1, 2) == deck[j].Mid(1, 2)) // 동일한 숫자(문자열)인지 검증
			{
				isSameNum++;
			}

		}
	}

	if (isDiffShape == 0) // 문양 모두 같을 때,  
	{
		int fistIdx = 0;
		int lastIdx = 0;

		fistIdx = _ttoi(deck[0].Mid(1, 2));
		lastIdx = _ttoi(deck[4].Mid(1, 2));
		if (deck[0] == L"C01.png" && deck[1] == L"C10.png" && deck[2] == L"C11.png" &&
			deck[3] == L"C12.png" && deck[4] == L"C13.png") // ACE 10 JACK KING QUEEN -> Royal Flush
		{
			pedigree.push_back(L"Royal Flush");
		}
		else if (lastIdx - fistIdx == 4) // ex 5 6 7 8 9 순차적인 5장의 패 마지막 인덱스와 첫번째 인덱스의 숫자 차이는 4!
		{
			
			pedigree.push_back(L"Straight Flush");
		}
		else // 그 외 5장의 같은 문양의 카드만 모인 경우
 		{
			pedigree.push_back(L"Flush");
		}
	}
	else  // 문양 1종류가 아닌 경우
	{
		CString max;
		CString min;

		int fistIdx = 0;
		int lastIdx = 0;


		vector<CString> strNums;


		for (int i = 0; i < 5; i++)
		{
			strNums.push_back(deck[i].Mid(1, 2));
		}

		sort(strNums.begin(), strNums.end());
		
		max = strNums[4];
		min = strNums[0];

		fistIdx = _ttoi(min.Mid(0, 2));
		lastIdx = _ttoi(max.Mid(0, 2));


		if (isSameNum == 6) // 같은 숫자가 2쌍
		{
			pedigree.push_back(L"Four of a kind");
		}
		else if (isSameNum == 4)
		{
			pedigree.push_back(L"Full House");
		}
		else if (isSameNum == 3)
		{
			pedigree.push_back(L"Triple") ;
		}
		else if (isSameNum == 2)
		{
			pedigree.push_back(L"Two Pair");
		}
		else if (isSameNum == 1)
		{
			pedigree.push_back(L"One Pair");
		}
		else if (isSameNum == 0 && (lastIdx - fistIdx == 4))  // 문양 상관없이 max-min = 4여야함.. 
		{
			pedigree.push_back(L"Straight");
		}
		else
		{
			pedigree.push_back(L"High Card");
		}
	}

	return pedigree;
}
```

<br>

straight를 제외한 나머지의 경우 카드 숫자에 상관없이 나오는 경우가 동일한 점을 이용해서.. 카운트된 횟수에 따라 경우를 나누었다. <br>
ex isSameNum -> 1 (원페어), 2 (투페어) ... 이런식으로 나누었음.. <br>
그리고 스트레이트까지 조건을 지정한 뒤 그 외 나머지 경우는 모두 하이카드에 해당하므로 `else`로 처리해두었다. <br>
straight의 경우에는 조금 까다로웠다... <br>
일단, 숫자가 모두 다른 점을 조건으로 걸고 추가로 순차적인 5장의 조합이기에 가장 큰 숫자와 가장 작은 숫자의 차가 4라는 것을 이용해서 로직을 작성했고 <br>
아래와 같이 코드를 작성했다. <br>
```cpp
CString max;
CString min;

int fistIdx = 0;
int lastIdx = 0;


vector<CString> strNums; // 숫자 문자열만 저장하기 위한 문자열 vector


for (int i = 0; i < 5; i++)
{
  strNums.push_back(deck[i].Mid(1, 2));  // 숫자 문자열 5개 저장
}

sort(strNums.begin(), strNums.end()); // 오름차순 정렬

max = strNums[4]; // 가장 큰 숫자 문자열
min = strNums[0]; // 가장 작은 숫자 문자열

fistIdx = _ttoi(min.Mid(0, 2)); // 정수형으로 변환 
lastIdx = _ttoi(max.Mid(0, 2));
```

<br><br><br>
* 전체 족보를 조회할 수 있는 화면을 넣을 것 <br>
처음에는 스크롤을 넣어 만들어보려고 했으나, 생각보다 자료가 없고 좋은 예시가 보이지않았다 ㅠㅠ <br>
그래서 tab으로 만들게 되었는데, 생각보다 족보들을 보기 편했다. <br>
게시해야 할 족보는 5장씩 10개 총 50장 일부 텍스트까지 포함하면 너비가 엄청 넓다.. <br>
tab을 활용했을 때는 그렇게까지 큰 공간을 차지하지 않는 것이 큰 장점이었다. <br>
아래의 사이트를 참고해 만들었다. <br><br>

<a href="https://balabala.tistory.com/36">TAB Dialog</a> <br>

1. TAB 메인 다이얼로그(혹은 호출될 자식 다이얼로그)에 추가한다. 및 탭화면으로 쓸 다이얼로그 추가 <br>
![1](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/2cdad363-abb1-48f0-b771-259e9429a016) <br><br>
2. 생성한 Dlg의 ID를 변경, 스타일: popup -> child, 시스템메뉴: true -> false, 제목 표시줄: true -> false<br>
 ![1](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/cfb417be-aa75-4335-91aa-d29ae6df9b63) <br><br>
3. 탭 전용으로 생성한 다이얼로그에 클래스 추가 (각 탭 전용 다이얼로그에 모두 적용) <br>
![4](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/f1656086-ba6b-475c-b8b5-bf49a74ded09) <br><br>
4. TAB Ctrl 멤버변수 추가 <br>
![5](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/09e5c46c-cd7c-4b62-83fd-cebeb11e67a1) <br><br>
5. class 마법사 -> 명령 -> "IDC_TAB_MAIN" 선택 -> TCN_SELCHANGE 선택 <br>
![6](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/f0b359a9-0c2d-425e-8cac-30c97aae80d1) <br><br>
6. TAB 메인 다이얼로그 클래스에 각 탭 전용 클래스들의 헤더 추가 <br>

```cpp
#pragma once
#include "afxdialogex.h"
#include "CDlgTab1.h" // 탭화면용 클래스 헤더파일들 추가 
#include "CDlgTab2.h"
#include "CDlgTab3.h"
#include "CDlgTab4.h"


// PedigreeDlg 대화 상자

class PedigreeDlg : public CDialogEx
{
  ...
}
```

<br>

7. TAB 메인 다이얼로그 클래스에 OnInitDialog (없으면 가상함수 추가)에 아래와 같이 코드 작성(초기설정, 탭선택이벤트 ) <br><br>
```cpp
BOOL PedigreeDlg::OnInitDialog() // 초기설정
{
	CDialogEx::OnInitDialog();

	// TODO:  여기에 추가 초기화 작업을 추가합니다.
	CRect rect;
	m_tab.GetWindowRect(rect);

	m_tab.InsertItem(0,L"족보1"); // 탭 이름 설정.
	m_tab.InsertItem(1,L"족보2");
	m_tab.InsertItem(2,L"족보3");
	m_tab.InsertItem(3,L"족보4");

	m_tab.SetCurSel(0);

	dlg1 = new CDlgTab1;
	dlg1->Create(IDD_DIALOG_TAB1,&m_tab);
	dlg1->MoveWindow(0, 20, rect.Width(), rect.Height());
	dlg1->ShowWindow(SW_SHOW); // 첫번째 탭을 show로 하고 나머지 hide

	dlg2 = new CDlgTab2;
	dlg2->Create(IDD_DIALOG_TAB2, &m_tab);
	dlg2->MoveWindow(0, 20, rect.Width(), rect.Height());
	dlg2->ShowWindow(SW_HIDE); // 첫번째 탭을 show로 하고 나머지 hide

	dlg3 = new CDlgTab3;
	dlg3->Create(IDD_DIALOG_TAB3, &m_tab);
	dlg3->MoveWindow(0, 20, rect.Width(), rect.Height());
	dlg3->ShowWindow(SW_HIDE); // 첫번째 탭을 show로 하고 나머지 hide

	dlg4 = new CDlgTab4;
	dlg4->Create(IDD_DIALOG_TAB4, &m_tab);
	dlg4->MoveWindow(0, 20, rect.Width(), rect.Height());
	dlg4->ShowWindow(SW_HIDE); // 첫번째 탭을 show로 하고 나머지 hide


	return TRUE;  // return TRUE unless you set the focus to a control
	// 예외: OCX 속성 페이지는 FALSE를 반환해야 합니다.
}

...

void PedigreeDlg::OnSelchangeTabMain(NMHDR* pNMHDR, LRESULT* pResult) // 탭 선택 이벤트 
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.
	if (IDC_TAB_MAIN == pNMHDR->idFrom) 
	{
		int select = m_tab.GetCurSel();
		switch (select)
		{
		case 0:
			dlg1->ShowWindow(SW_SHOW);
			dlg2->ShowWindow(SW_HIDE);
			dlg3->ShowWindow(SW_HIDE);
			dlg4->ShowWindow(SW_HIDE);
			break;
		case 1:
			dlg1->ShowWindow(SW_HIDE);
			dlg2->ShowWindow(SW_SHOW);
			dlg3->ShowWindow(SW_HIDE);
			dlg4->ShowWindow(SW_HIDE);
			break;
		case 2:
			dlg1->ShowWindow(SW_HIDE);
			dlg2->ShowWindow(SW_HIDE);
			dlg3->ShowWindow(SW_SHOW);
			dlg4->ShowWindow(SW_HIDE);
			break;
		case 3:
			dlg1->ShowWindow(SW_HIDE);
			dlg2->ShowWindow(SW_HIDE);
			dlg3->ShowWindow(SW_HIDE);
			dlg4->ShowWindow(SW_SHOW);
			break;
		default:
			break;
		}
	}
	*pResult = 0;
}
```

<br><br><br>

* 자유 추가 기능 구현(ex 10000번 수행 후 족보의 확률 분석...) <br>
앞선 문자열벡터를 반환하는 것과는 다르게, 이번엔 edit ctrl에 문자열 게시를 위해 정수형 벡터를 반환 
```cpp
vector<int> RecordDlg::DiscriPedigree(int n) // ex 1000;
{
	// TODO: 여기에 구현 코드 추가.
	
	int nRF = 0;
	int nSF = 0;
	int nFL = 0;
	int nFK = 0;
	int nFH = 0;
	int nTR = 0;
	int nTP = 0;
	int nOP = 0;
	int nST = 0;
	int nHC = 0;
	vector<int> nPedigree = {nRF,nSF,nFL,nFK,nFH,nTR,nTP,nOP,nST,nHC}; // 각 족보 카운트

	srand((int)time(NULL)); // 반복문 외부에서 초기화!!!

	for (int i = 0; i < n; i++) 
	{
		int temp = 0;
		
		index = { (rand() % 52), (rand() % 52), (rand() % 52), (rand() % 52), (rand() % 52) }; // 여기서 여러번 반복됨.. 

		for (int i = 0; i < 5; i++) // 중복 방지 로직
		{
			temp = index[i];
			for (int j = i+1; j < i; j++)
			{
				if (index[j] == temp)
				{
					index[i] = (rand() % 52);
					i--;
				}
			}
		} // 여기 로직 다시 짜기.. 

		vector<CString> deck; // 뽑은 5장의 카드 경로를 저장하는 CString Vector

		for (int i = 0; i < 5; i++)
		{
			deck.push_back(Routes[index[i]]); // 순차적으로 deck에 삽입
		}

		sort(deck.begin(), deck.end()); // 오름차순 정렬
		
			int isDiffShape = 0;
			int isSameNum = 0;

		for (int i = 0; i < 4; i++)
		{
			for (int j = i + 1; j < 5; j++)
			{
				if (deck[i].Mid(0, 1) != deck[j].Mid(0, 1)) // 동일한 문양인지 검증
				{
					isDiffShape++;
				}

			}
		}

		for (int i = 0; i < 4; i++)
		{
			for (int j = i + 1; j < 5; j++)  // 1 2 2 1 2 기대값 4... 1 + 3 = 4 같은 숫자 2쌍일 때 풀하우스   
			{								 // 1 2 3 3 4 기대값 1... 0 + 1 = 1 원페어
											 // 1 3 3 4 4 기대값 2... 1 + 1 = 2 투페어
											 // 1 2 2 2 3 기대값 3... 2 + 1 = 3 트리플
											 // 1 1 1 1 4 기대값 6... 3 2 1 = 6 .. 포카드 
											 // 1 2 3 4 5 기대값 0 .. max-min = 4 스트레이프
											 // 나머지 경우 하이카드 
				if (deck[i].Mid(1, 2) == deck[j].Mid(1, 2)) // 동일한 숫자(문자열)인지 검증
				{
					isSameNum++;
				}

			}
		}

		if (isDiffShape == 0) // 문양 모두 같을 때,  
		{
			int fistIdx = 0;
			int lastIdx = 0;

			fistIdx = _ttoi(deck[0].Mid(1, 2));
			lastIdx = _ttoi(deck[4].Mid(1, 2));
			if (deck[0] == L"C01.png" && deck[1] == L"C10.png" && deck[2] == L"C11.png" &&
				deck[3] == L"C12.png" && deck[4] == L"C13.png")
			{
				nPedigree[0]++;
			}
			else if (lastIdx - lastIdx == 4)
			{
				nPedigree[1]++;
			}
			else
			{
				nPedigree[2]++;
			}
		}
		else  // 문양 1종류가 아닌 경우
		{
			CString max;
			CString min;

			int fistIdx = 0;
			int lastIdx = 0;


			vector<CString> strNums;


			for (int i = 0; i < 5; i++)
			{
				strNums.push_back(deck[i].Mid(1, 2));
			}

			sort(strNums.begin(), strNums.end()); // 00~13 형식의 숫자(문자열)들을  오름차순 정렬

			max = strNums[4];
			min = strNums[0];


			fistIdx = _ttoi(min.Mid(0, 2));
			lastIdx = _ttoi(max.Mid(0, 2));


			if (isSameNum == 6) // 같은 숫자가 2쌍
			{
				nPedigree[3]++;
			}
			else if (isSameNum == 4)
			{
				nPedigree[4]++;
			}
			else if (isSameNum == 3)
			{
				nPedigree[5]++;
			}
			else if (isSameNum == 2)
			{
				nPedigree[6]++;
			}
			else if (isSameNum == 1)
			{
				nPedigree[7]++;
			}
			else if (isSameNum == 0 && (lastIdx - fistIdx == 4))  // 문양 상관없이 max-min = 4여야함.. 
			{
				nPedigree[8]++;
			}
			else
			{
				nPedigree[9]++;
			}
		}
	}
	return nPedigree;
}
```

<br>

위의 메서드에서 반환한 시행회수에 따른 각 족보의 확률과 시행횟수를 통해 시뮬레이터의 edit ctrl에 각 확률 및 시행횟수를 문자열로 출력 <br>

```cpp
void RecordDlg::OnClickedButtonSim()
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다.

	CString getCount;
	int nCount = 0;
	 
	GetDlgItemText(IDC_EDIT_COUNT,getCount);
	nCount = _ttoi(getCount);

	if (!isnan((double)nCount))  // 숫자가 아닌 값을 입력할 시 예외처리 
	{
		MessageBox(L"숫자를 입력해주세요!");
		nCount = 1; // 기존의 입력을 무시하고 카운트 1로 초기화 
	}

	DiscriPedigree(nCount); // edit에 입력한만큼 반복 수행 
	
	vector<double> probPedigree;

	CString probRF; // 각 족보에 해당하는 확률을 edit ctrl에 표시할 문자열
	CString probSF; 
	CString probFL;	
	CString probFK;	
	CString probFH;	
	CString probTR;	
	CString probTP;	
	CString probOP;	
	CString probST;	
	CString probHC;	

	vector<CString> strProbability = 
	{
		probRF, 
		probSF, 
		probFL,
		probFK,
		probFH,
		probTR,
		probTP,
		probOP,
		probST,
		probHC
	};

	CString nRF;
	CString nSF;
	CString nFL;
	CString nFK;
	CString nFH;
	CString nTR;
	CString nTP;
	CString nOP;
	CString nST;
	CString nHC;

	vector<CString> nPedigree =
	{
		nRF,
		nSF,
		nFL,
		nFK,
		nFH,
		nTR,
		nTP,
		nOP,
		nST,
		nHC
	};


	for (int i = 0; i < 10; i++)
	{
		nPedigree[i].Format(L"%d", DiscriPedigree(nCount)[i]); // 횟수에 따른 각 족보가 등장한 횟수를 문자열로 변환
		probPedigree.push_back((double)DiscriPedigree(nCount)[i] / nCount); // 각 족보가 등장한 확률을 저장
		strProbability[i].Format(L"%f", probPedigree[i]); // 각 족보가 등장한 확률을 문자열로 변환
	}

	SetDlgItemText(IDC_EDIT_RF,(strProbability[0] + L"%" + L"(" + nPedigree[0] + L")")); // 확률 ( 족보 등장 횟수) 
	SetDlgItemText(IDC_EDIT_SF,(strProbability[1] + L"%" + L"(" + nPedigree[1] + L")"));
	SetDlgItemText(IDC_EDIT_FL,(strProbability[2] + L"%" + L"(" + nPedigree[2] + L")"));
	SetDlgItemText(IDC_EDIT_FK,(strProbability[3] + L"%" + L"(" + nPedigree[3] + L")"));
	SetDlgItemText(IDC_EDIT_FH,(strProbability[4] + L"%" + L"(" + nPedigree[4] + L")"));
	SetDlgItemText(IDC_EDIT_TK,(strProbability[5] + L"%" + L"(" + nPedigree[5] + L")"));
	SetDlgItemText(IDC_EDIT_TP,(strProbability[6] + L"%" + L"(" + nPedigree[6] + L")"));
	SetDlgItemText(IDC_EDIT_OP,(strProbability[7] + L"%" + L"(" + nPedigree[7] + L")"));
	SetDlgItemText(IDC_EDIT_STR,(strProbability[8] + L"%" + L"(" + nPedigree[8] + L")"));
	SetDlgItemText(IDC_EDIT_HC,(strProbability[9] + L"%" + L"(" + nPedigree[9] + L")"));

	MessageBox(L"Done!"); // 수행 완료 알림
}
```

* 수행 기록을 txt파일로 저장 및 출력..  <br>
사실 이 부분의 경우에는 좀 더 공부해보고 추후에 제대로 정리를 할 예정이다.<br>
솔직히 너무 붙여쓴 느낌이 강해서 공부가 필요한 부분이다... <br>
```cpp
void RecordDlg::OnClickedButton2() // Load 텍스트 파일을 불러와야함.. 
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다. LOAD
	CString str;
	FILE* m_pFile;
	TCHAR BASED_CODE szFilter[] = _T("텍스트 파일(*.TXT) | *.TXT;*.txt; | 모든 파일(*.*) |*.*|");
	CFileDialog dlg(TRUE, _T("*.txt"), 0, OFN_HIDEREADONLY | OFN_OVERWRITEPROMPT, szFilter); // 읽기 전용.. 
	

	if (dlg.DoModal() == IDOK) 
	{
		m_strPath = dlg.GetPathName();

		
		errno_t err = _tfopen_s(&m_pFile, m_strPath, _T("rt,ccs=UNICODE"));
		if (err != 0) { return; }
		/*CStdioFile m_File(m_pFile);*/
		CFile file;
		CFileException e;
		if (!file.Open(m_strPath, CFile::modeRead | CFile::shareDenyNone, &e))
		{
			e.ReportError(); // error 
		}

		ShellExecute(NULL,L"open",m_strPath,NULL,NULL,SW_SHOW);

		/*m_File.ReadString(str);*/
		
	}
}


void RecordDlg::OnClickedButton3() // save
{
	// TODO: 여기에 컨트롤 알림 처리기 코드를 추가합니다. SAVE
	CString str1, str2, str3, str4, str5, str6, str7, str8, str9, str10;
	FILE* m_pFile;
	TCHAR BASED_CODE szFilter[] = _T("텍스트 파일(*.txt) | *.TXT;*.txt; | 모든 파일(*.*) |*.*|");
	CFileDialog dlg(FALSE, _T("*.txt"), 0, OFN_HIDEREADONLY | OFN_OVERWRITEPROMPT, szFilter); // 읽기 전용|쓰기 가능.. 

	if (dlg.DoModal() == IDOK)
	{
		m_strPath = dlg.GetPathName();

		errno_t err = _tfopen_s(&m_pFile, m_strPath, _T("wt,ccs=UNICODE"));
		if (err != 0) { return; }
		CStdioFile m_File(m_pFile);

		MessageBox(m_strPath); // 저장된 경로 알림


		GetDlgItemText(IDC_EDIT_RF, str1); // 텍스트 박스에서 글자 가져오기
		GetDlgItemText(IDC_EDIT_SF, str2); 
		GetDlgItemText(IDC_EDIT_FL, str3); 
		GetDlgItemText(IDC_EDIT_FK, str4); 
		GetDlgItemText(IDC_EDIT_FH, str5); 
		GetDlgItemText(IDC_EDIT_TK, str6); 
		GetDlgItemText(IDC_EDIT_TP, str7); 
		GetDlgItemText(IDC_EDIT_OP, str8); 
		GetDlgItemText(IDC_EDIT_STR, str9); 
		GetDlgItemText(IDC_EDIT_HC, str10); 

		m_File.WriteString(L"Royal Flush: "+str1+L"\n");
		m_File.WriteString(L"Straight Flush: "+str2+L"\n");
		m_File.WriteString(L"Flush: "+str3+L"\n");
		m_File.WriteString(L"Four of a kind: "+str4+L"\n");
		m_File.WriteString(L"Full House: "+str5+L"\n");
		m_File.WriteString(L"Three of a kind(Triple): "+str6+L"\n");
		m_File.WriteString(L"Two Pair: "+str7+L"\n");
		m_File.WriteString(L"One Pair: "+str8+L"\n");
		m_File.WriteString(L"Straight: "+str9+L"\n");
		m_File.WriteString(L"High Card: "+str10+L"\n");

		m_File.Close();
	}
} 
```
<br>

↓ 입력횟수 만큼 로직 반복 실행 화면 <br>
![10000번수행확률](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/d0d1336e-eb92-4f8f-b59f-f099d8c7129e) <br><br>

↓ 저장 버튼 입력후 파일 저장 <br>
![기록저장화면](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/e507bb13-5f10-42cb-a505-990616726530) <br><br>

↓ 열기 버튼 입력 후 파일 로드 <br>
![기록파일출력화면1](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/bc9c41d0-cf6e-44ed-bc75-e323297e0269) <br><br>

↓ 실행된 파일 <br>
![기록파일출력화면2](https://github.com/jackerbell/jackerbell.github.io/assets/65724413/faefec96-922a-4d25-b9af-12750545e6a0) <br><br><br>

## 리뷰
처음 보는 기능들을 연속적으로 추가하다보니, 이론을 제대로 알고 넣었다기 보다는 이것저것 테스트해보고 급하게 붙여넣은 느낌이 강했다. 
처음 프로젝트 명도 주제와 맞지 않아 중간에 따로 고쳤고, 무엇보다 모듈화가 제대로 되지 않았다. 
그 밖에 예외처리라던가 모듈의 개별적인 조정 등 적당한 형태로 만든 느낌이 강해서 보완할 점이 많았다. 추후 다시 만들어볼 떄, 
열거형, 다중 상속 등 좀 더 고급 개념을 활용해 지금보다 더 코드의 로직을 간결하게 만드는게 지금의 목표다. 






