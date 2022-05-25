UUserWidget  

UFUNCTION( ... )  
BlueprintCallable  
Category = "UMG_Game"  
ChangeMenuWidget  
TSubclassOf<UUserWidget>  

UPROPERTY( ... )  
EditAnywhere  
BlueprintReadOnly  

UPROPERTY()  
UUserWidget* CurrentWidget;  

Super::  
  
ConstructorHelpers::FObjectFinder<USkeletalMesh> SM(TEXT("경로이름'"));  

---
  
**헤더 파일 포맷**  
- 대부분 .cpp 클래스와 똑같이 이루어지만, 일부 구조를 지켜야 언리얼 엔진에서 정상 작동한다.
- #include "클래스이름.generated.h"
- : public UObject
- GENERATED_BODY()

---
  
**Tarray:**
- C++의 std::vector와 비슷한 역할을 하는 언리얼의 동적 배열이다.
- 엔진에서 가장 간단하고 자주 쓰이는 컨테이너 클래스이다.
- 신속성, 메모리 효율성, 안전성을 목표로 설계되었다.
- 유형이 같은 다른 오브젝트를 순서대로 정리하여 담아두는 역할(=배열)을 한다.
- TArray는 값 유형으로, int32나 float 같은 값 유형과 비슷하다.  
- 선언방법예시: TArray<int32> IntArray; TArray<FString> StrArray;  
- TArray 클래스의 함수들 엿보기  
추가: Add/Emplace/Push/Append/Insert   
정렬: Sort   
제거: Remove/RemoveSingle/RemoveAt/RemoveAll/Empty   
크기 설정: SetNum  
갯수: Num()  
접근: [], Top(), Last()  
검사: IsValidIndex()  
검색: Find()  
기존 배열을 힙으로 변환: Heapify   

---
  
**int8, int16, uint8?**
- 뒤에 붙는 숫자는 표현할 수 있는 범위를 의미한다.  
- 'u'는 unsigned. 부호(음수 영역)가 없음을 의미한다.  
  
예) int8은 int(정수)형의 8비트. 2^8개(=256)개의 정수를 표현할 수 있다.  
예2) float32는 부호/지수/가수 부분으로 나뉜다.
  
---

**std::string c_str():**  
반환값: const char*  
c++의 string을 c스타일의 문자열로 바꿀때 사용한다.  
  
---
  
- 자료형마다 차지하는 메모리 크기가 다르다.     
자료형 크기 예) char(1Byte), signed int (4Byte), unsigned long (4Byte)    

---
  
**reinterpret_cast:**  
- C++에서 제공하는 형변환(cast) 객체 중 하나.
- 해당 자료형의 bit수에 맞게 바꾼다.
- 자료를 bit 단위 그대로 변수에 전달한다.

예1)  int * -> long -> int *: 서로 4Byte로 같으므로 데이터가 유지됨  
예2) int * -> char -> int *: 서로 크기가 다르므로 변환하면 데이터가 파괴됨  
- 주로 패킷통신할 때 자료를 포인터로 받아올 때 사용한다.  

사용예시)  
int * -> long -> int * 로 형변환하는 경우  
int* p = new int(100);  
long c = reinterpret_cast<int>(p);  

---
  
- 포인터의 크기는 실행 파일이 컴파일된 아키텍쳐에 따라서 달라진다.  
32bit 실행 파일은 32bit 메모리 주소를 사용하므로 -> 포인터의 크기: 32bit  
64bit 실행 파일은 64bit 메모리 주소를 사용하므로 -> 포인터의 크기: 64bit  
int*, float*, char* 무엇이든 포인터는 주소를 저장하는 자료형이다. 그러므로 포인터의 크기는 자료형에 상관 없이 같은 아키텍쳐 안에서는 항상 같다.  

---
  
**TCHAR**  
요즘은 문자를 처리할 때 Unicode를 주로 사용한다. (2Byte)  
초창기에 문자열 처리는 ASCII코드로 사용하고 있고, 지금도 사용하고 있다. (1Byte)  

C/C++에선 ASCII코드와 Unicode를 사용면서 문자열 처리에 1Byte와 2Byte 메모리 할당에 신경써야 했다.  

char(1Byte): ASCII를 사용하는 프로그램  
wchar_t (2Byte): Unicode를 사용하는 프로그램 (Wide Char_Text)   

MS에서 자료형 표시에 일관성을 부여하기 위해 자료형들을 대문자로 사용한다.  
char -> CHAR  
wchat_t -> WCHAR  
 
ASCII코드로 사용된 프로그램에서 Unicode를 사용하거나, Unicode로 사용된 프로그램에서 ASCII코드 사용할 때,  
CHAR, WCHAR를 경우에 따라 나누지 않고 통일시킨 자료형을 사용한다. -> TCHAR(Text Character)  

---
  
**sstream(StringStream)**   
- 여러가지 자료형이 한 줄에 들어오면 파싱해서 용도에 맞게 사용하기 위한 라이브러리다.    
예) "이름/날짜/내용"과 같이 문자열로 한 줄의 데이터로 들어오면 각각 이름, 날짜, 내용으로 파싱한다.  
  
---
  
UCLASS() 매크로: 블루프린트에 게임플레이 요소 노출시키기  
Blueprintable: C++클래스를 블루프린트를 만들 수 있게 노출시키기  
BlueprintType:  C++클래스를 블루프린트에서 변수로 사용 가능한 유형(Type)으로 노출시키기  
NotBlueprintable: C++클래스를 블루프린트로 만들 수 없게 지정하기  
BlueprintReadOnly: 해당 프로퍼티를 블루프린트에서 읽기만 가능하게 만들기(변경X)  
BlueprintReadWrite: 해당 프로퍼티를 블루프린트에서 읽고 쓸 수 있게 만들기  
BlueprintAssignable: 해당 프로퍼티를 블루프린트에서 할당 가능하도록 노출시키기  
BlueprintCallable: 해당 프로퍼티를 블루프린트 그래프에서 호출 가능하도록 노출시키기  

---
  
AddOnScreenDebugMessage  
CreateDefaultSubobject<UPointLightComponent>  
다이나믹 델리게이트 AddDynamic  
UPROPERTY(VisibleAnywhere): 헤더파일에 선언한 컴포넌트가 에디터에서 디테일 탭에 보이게 한다.  

---

**memcpy(데이터가 복사될 곳의 주소, 복사할 데이터들이 위치한 주소, 복사할 데이터의 바이트 수)**
- 복사될 길이만큼 크기가 충분해야 한다.  
- \0 문자까지 복사가 되었는지 확인해야 한다. 그러므로 복사할 길이의 1만큼(\0의 길이) 더해야 한다.  

---
  
size_t: 데이터 타입. 반드시 unsigned형. 해당 시스템(32/64비트)에서 어떤 객체나 값이 포함할 수 있는 최대 크기의 데이터를 표현하는 타입.  
c/c++의 변수의 크기는 컴퓨터 환경에따라 다르다.  int형의 크기가 컴퓨터의 환경에 따라 달라진다. -> size_t를 사용하면, 어떤 환경에서든 4Byte의 크기(32bit unsigned int)로 고정된다.  
void *: void 형 포인터. 현재 가리키고 있는 대상체가 정해져 있지 않는 포인터. 형 변환 없이 어떠한 형의 포인터 변수도 넣을 수 있다.  

---
  
**bool 함수 코딩 스타일에 대한 고찰!**  
bool 형 리턴 값을 가지는 함수는   
무조건 그 함수가 하려는 일이 성공하면 true,   
아니면 false를 반환하게 하는 것이 올바르다.  

그래야 나중에 헷갈리지 않게 가독성을 높일 수 있다.  

ex)  
const ECODE EOK = 0; (false)  
에러 확인은  
if (!함수(...)) 식이 아니라,   
if (함수(...) == EOK) 식으로 비교하게 해서 가독성을 높인다.  

---
  
[C++ 11] 범위 기반 for문 :(콜론)  

int array = {1, 2, 3, 4, 5}  
for (int i : array) { 내용 }  
- i가 array의 요소 한개씩을 차례로 받아 반복문을 수행한다.  
- auto 키워드를 사용해서 C++이 자료형을 추론하도록 하는 것이 이상적이다.  
  
---
  
**C++ STL map**
- map의 원소는 pair<key/value>로 이루어져 있다. (key/value가 한 쌍)  
- 이진 탐색 트리(red-black)로 구성되어 있다.  
- pair 객체를 만들어서 key값을 기준으로 원소를 추가/삭제한다.  
- key값을 index로 사용하여 value에 접근할 수 있다. 배열처럼 [ ]로 접근이 가능하다.    
    
메모리가 연속되어 저장되어 있지 않다.  
찾고자 하는 원소를 빨리 찾기 위해 사용한다. (배열보다 빠르다)   
원소들이 항상 정렬된 상태가 되도록 하는 데 시간을 더 써서 찾는 시간을 단축한다.   


  
