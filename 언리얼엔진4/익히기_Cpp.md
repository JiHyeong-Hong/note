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
