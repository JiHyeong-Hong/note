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
