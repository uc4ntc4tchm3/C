### In C pass-by-reference is not exist



```
/* The C Programing Language - Dennis Ritchie */
page22
... In C, all function arguments are passed by value ...
```

c 언어에서 함수의 인자들은 모두 값으로 넘겨진다.

```
/* Wikipedia */
Call by reference
... This typically means that the function can modify the variable used as argument ...
```

Wikipedia 의 call-by-reference(이하 pass-by-reference) 에 관한 설명에서,"pass-by-reference란 일반적으로 함수 내에서 인자로 주어진 변수의 값을 변경할 수 있어야 한다."  라고 서술하고 있다.

즉, 함수 내에서 arguments의 값을 변경 할 수 있어야 진정한 의미의 pass-by-reference라고 할 수 있다. 

```
/* Concepts of Programing Language (10th Edition) */
(a) In mode
caller(a) ---- call ----> callee(x)

(b) Out mode
caller(b) <--- return --- callee(y)

(C) Inout mode
caller(c) <- call & return -> callee(z)
```

매개변수 전달법의 semantics model은 위의 Concept of Programing Language 의 Semantics Models of Parameter Passing 에서 언급한 것에서 알 수 있듯이 3가지가 존재한다.

(a) function call 당시 매개변수인 x의 값이 parameter a의 값으로 되는 것 - In mode

(b) function return 당시 argument b의 값이 parameter y의 값으로 되는 것 - Out mode

(c) function call 당시 매개변수인 z의 값이 argumnet인 c의 값으로 되고, function return 당시 argument인 c의 값이 parameter인 z의 값으로 되는 것 - Inout mode



이 때 C언어는 (a)인 In mode만 해당된다. 



```
/* Concepts of Programing Language (10th Edition) */
Pass-by-reference
...
```

위에서 언급한 내용을 정리하면 다음과 같다

(a) pass-by-reference는 Inout model 중 하나이다.

(b) pass-by-reference는 argument가 있는 storage에 access 할 수 있는 address(access path)를 전달한다.

(c) call 된 function 내에서 argument에 접근하는 것이 허용된다.



```
/* Wikipedia */
pass-by-reference
... pass-by-refernce can be simulated in languages ... 
languages such as C and ML use this technique. it is not a seperate evaluation strategy-the language calls by value- but sometimes it is referred to as call by address
```

마지막으로 Wikipedia의 pass-by-reference에 대해 서술한 내용을 보면

pass-by-reference를 흉내 낼 수 있으며 C와 ML 같은 언어에서 이와 같은 기술을 사용하며

또한 이것은 별개의 evaluation strategy 가 아닌 call by value라고 설명하고 있다. 

즉, pointer을 사용해서 pass-by-reference를 simulate한다고 해도 call-by-value라는 것이다.



```c
/* swap function in c */

void swap(int *a, int *b){
  int temp = *a;
  *a = *b;
  *b = temp;
}
```

```c++
/* swap function in c++ */

void swap(int &a, int &b){
  int temp = a;
  a = b;
  b = a;
}
```

위의 두 swap function를 비교하면 보다 명확하게 알 수 있다. in mode만 가능한 `c`에서는 값을 pointer type로 전달하고 (*)operator를 사용하여 pass-by-reference를 simulate 할 뿐이다. 반면에 pass-by-reference가 존재하는 `c++`의 경우 function의 parameter로 address를 전달하고 function 내에서 argument에 접근하여 modify 할 수 있다.



> **summary**
>
> c 언어에서 pass-by-reference는 존재 하지 않으며 어디까지나 call-by-value로 address 값을 넘기는 방식에 대한 별명일 뿐, 결국은 call-by-value 이다.