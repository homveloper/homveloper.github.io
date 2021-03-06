---
title: "전문가를 위한 C++ - 포인터"
excerpt: ""
categories:
    - "excpp"
tags:
    - [C++, Expert C++, Pointer]

sitemap:
    changefreq: daily

date: 2021-03-31
---

> 게임 개발자가 되기 위해 공부하면서 배우는 여러가지 내용들을 기록하기 위한 블로그입니다. 포스팅에 참고한 모든 강의와 자료들은 하단에 "참조"에 남겨두었습니다.
> 
> 본 포스팅은 마크 그레고리의 "전문가를 위한 c++"의 내용을 정리하였습니다.

## 포인터

<b><sub>Pointer</sub></b>

C++ 어플리케이션의 메모리는 스택<sub>Stack</sub>과 힙<sub>Heap</sub> 두 영역을 나누어져 있습니다. 

스택은 함수의 호출과 관계되는 지역 변수와 매개 변수가 저장되는 영역입니다. 힙은 사용자가 명시적으로 메모리에 할당할 수 있는 영역입니다. 즉, 사용자가 메모리 공간을 동적으로 할당하고 해제합니다.

힙에 값을 넣으려면 메모리를 할당해야 하지만, 그전에 포인터를 먼저 선언해야 합니다.

```cpp
int* pInt;
```


int 타입 뒤의 ```*```은 선언하는 변수가 일부 정수 메모리를 참조하거나 가리킨다는 것을 의미합니다. 

초기에는 아무것도 할당하지 않았기 때문에, 특정한 변수를 가리키지 않습니다. 즉, 초기화되지 않은 포인터 변수입니다. 

초기화되지 않은 변수는 조심해야 합니다. 특히 포인터는 메모리의 임의의 위치를 가리키기 때문 입니다. 위의 방식으로 포인터를 선언하게 되면 프로그램이 충돌할 가능성이 높습니다.

### 널 포인터

그렇기에 항상 포인터를 선언함과 동시에 초기화를 해야 합니다. 메모리를 할당하고 싶지 않다면 **널 포인터<sub>nullptr</sub>**로 초기화 할 수 있습니다.

다음 코드는 다음 내용에 대한 예시입니다.

```cpp
int* pInt1;             // X, 아무 공간을 가리키고 있음.
int* pInt2 = nullptr;   // O

cout<<pInt1<<endl;
cout<<pInt2<<endl;
```

```console
0x21199c124c0
0
```

널 포인터는 포인터가 가질수 있는 특별한 기본값이며, false로 변환됩니다. 부울 표현식에서 아래와 같이 사용될 수 있습니다.

```cpp
if(!pInt2){ /* TODO */}
if(nullptr != pInt2){ /* TODO */}
```

## 동적 할당

힙 영역에 메모리를 동적으로 할당하기 위해서는 ```new``` 연산자로 할 수 있습니다.

```cpp
int *pInt = new int;
```

```pInt```는 하나의 정수 값 주소를 가리키는 포인터입니다. 이 값에 접근하려면 포인터를 역참조해야 합니다. 역참조는 ```*``` 연산자를 사용합니다. 다음 코드는 새로 할당된 포인터에 값을 설정합니다.

```cpp
*pInt = 12;
```

이는 ```pInt```의 값 12를 설정하는 것이 아닌, 포인터가 가리키고 있는 메모리 주소의 값을 12로 설정합니다. 

동적으로 할당된 메모리를 사용한 후에는 ```delete``` 연산자를 이용해 메모리 할당을 해제해야 합니다. 할당을 해제한 후 포인터가 사용되지 않으려면 nullptr로 설정하는 것이 좋습니다.

```
delete pInt;
pInt = nullptr;
```

> 포인터에 역참조를 하기 전에 해당 포인터가 유효한지 확인해야 합니다. 널포인터 또는 초기화되지 않은 포인터를 역참조하면 오동작이 발생하게 됩니다. 

포인터는 힙 메모리 이외에도 스택의 변수, 다른 포인터를 가리키는 포인터를 선언할 수도 있습니다. 특정 변수에 대한 주소를 얻으려면 ```&``` 연산자를 사용합니다.

```cpp
int i = 12;
int* pInt = &i;     // 변수 i의 주소를 가리킴
```

C++은 구조체<sub>Struct</sub>에 대해 포인터 연산을 위한 특별한 구문이 있습니다. 구조체에 대해 포인터가 있는 경우 먼저 * 연산자로 역참조한 다음 해당 필드에 접근할 수 있습니다. 

```cpp
Employee* employee = GetEmployee();
cout<<(*employee).GetSalary()<<endl;
```

이 구문은 ```->``` 연산자를 사용하면 역참조와 필드 접근을 한번에 수행할 수 있습니다. 다음 코드는 앞의 코드와 동일하지만, 간결합니다.

```cpp
Employee* employee = GetEmployee();
cout<<employee->GetSalary()<<endl;
```

## 참조

- 전문가를 위한 C++