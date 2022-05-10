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

  
