MarshalAs  
- 마샬링 동작을 커스텀화한다.
- 매니지드 코드(.NET 기반 언어, C#) <--> 언매니지드 코드(C/C++) 간의 데이터를 마샬링하는 방법을 알려주는 역할을 한다.
- 두 코드 간에 데이터를 전송하기 위해서 각 코드의 데이터 타입을 마샬링 해줘야 한다.  

Parse()  
- string 타입 데이터를 int/float 타입으로 변환시킨다.  
ToString()  
- int/float 타입 데이터를 string 타입으로 변환시킨다.  

---

GetIniValue  
GetPrivateProfileString  
StringBuilder / String  

---

제네릭 타입  
 - C++ 템플릿 개념과 비슷.
 - int, float, double과 같은 자료형들을 확정하지 않고, 자료형 자체를 Type Parameter로 받아들이도록 클래스를 정의한다.  
 - 클래스의 거의 모든 부분이 동일한데, 일부 자료형만이 다른 경우에 사용한다.  
 - 클래스, 인터페이스, 메서드 등에 <T> 같은 타입 파라미터를 붙여 구현한다.  
