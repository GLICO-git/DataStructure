<!--
1. 이미지(가운데 정렬, 60%)
<centet><img src="이미지링크" width="60%"/></center>

1-2. 이미지 캡션 달기
<p align = "center">
내용
</p>

2. 글꼴 색상
노란색 : #fff5b1
초록색 : #dcffe4
주황색 : #f7ddbe
<span style="color: #fff5b1">
</span>
-->
# 제목
## Contents
 1. [배열(Array)](#배열(Array))
    - [배열 요소의 저장](#배열-요소의-저장)
    - [다차원 배열](#다차원-배열)
 1. [스택(Stack)](#스택(Stack))
    - [스택의 연산](#스택의-연산)
    - [배열을 이용한 스택의 구현](#배열을-이용한-스택의-구현)
    - [Push()](#Push())
    - [Pop()](#Pop())
    - [Peek()](#Peek())
1. [큐(Queue)](#큐(Queue))
    - [큐의 연산](#큐의-연산)
    - [선형 큐와 원형 큐](#선형-큐와-원형-큐)
        - [선형 큐](#선형-큐)
        - [원형 큐](#원형-큐)
            - [원형 큐의 삽입 삭제 구현](#원형-큐의-삽입-삭제-구현)
1. [리스트(List)](#리스트(List))
    - [선형 리스트](#선형-리스트)
    - [연결 리스트](#연결-리스트)
        - [단순 연결 리스트의 구현](#단순-연결-리스트의-구현)
        - [단순 연결 리스트의 삽입 연산 구현](#단순-연결-리스트의-삽입-연산-구현)
        - [단순 연결 리스트의 삭제 연산 구현](#단순-연결-리스트의-삭제-연산-구현)

***
# 배열(Array)
- 같은 데이터형(Data type)을 가진 원소가 순서적으로 구성된 집합
- 자료구조를 연속적인 기억 장소에 저장함
- 배열을 대표하는 한 개의 변수명과 첨자로 표현함
- 배열을 구성하는 각각의 자료는 요소(element)라고 하며, 배열 요소는 모두 같은 자료형을 갖는다 (정수형 int, 실수형 float, double)
- 첨자는 몇 번째 요소를 사용할 것인가를 나타내는 색인(index)이다
`int Array[5];      // 자료형(정수형) 배열명[첨자];`
***
## 배열 요소의 저장
- `a`는 시작 위치, `k`는 자료형의 크기를 나타낸다면 요소들의 주소를 계산할 수 있다
```
A[0] : a
A[1] : a + k
...  : ...
A[i] : a + (i * k)
...  : ...
```
***

## 다차원 배열
- 1차원 배열을 여러 개 쌓아 놓은 것이 2차원 배열이며, 
- 2차원 배열을 여러 개 쌓아 놓은 것이 3차원 배열이다
<br> - 2차원 배열의 요소는 i와 j 두 개의 첨자로 구분 된다
<br>첨자 i에 해당하는 것을 `행(row)`이라 하고, j에 해당하는 것을 `열(Column)`이라 한다

# 스택(Stack)
- 삽입과 삭제가 한쪽 끝에서만 발생하는 선형 리스트이다
- 자료의 삽입과 삭제가 발생하는 부분을 `top`라는 포인터가 가리키며 항상 제일 위에 있는 자료를 가리킨다
***
## 스택의 연산
- `Push 연산` : 자료를 삽입
- `Pop 연산` : 자료를 삭제
- `Peek 연산` : top포인터가 가리키는 자료의 내용을 조사

- 스택에서의 자료의 삽입은 `top`포인터가 가리키는 위치보다 1이 증가한 위치에 자료가 삽입되고, 삭제는 `top`포인터가 가리키는 위치의 자료가 삭제 된다<br>
<br>->
즉, 이 두 연산은 `top`을 변환시켜 연산을 하며 Push = top + 1이 되고 Pop = top - 1이 된다

## 배열을 이용한 스택의 구현
```c
#define MAX_SIZE 5              // 스택 사이즈 5로 정의
typedef int element;            // int형을 스택 element의 자료형으로
element stack[MAX_SIZE];        // 자료 형 element를 저장할 수 있는 공간을 스택 사이즈만큼
int top = -1;                   // 스택의 top 초기 값을 -1로 저장하여 공백 상태로
```
***
## Push()
- `Push()`연산은 스택에 새로운 자료를 추가하는 연산이다
- 이 연산은 스택의 맨 위에서만 수행되므로 `A(인덱스 : 0)`, `B(인덱스 : 1)` 두 개의 자료가 이미 저장되어 있다면 `C`를 스택에 추가할 때 인덱스는 2가 된다<br>
+) 위에서 스택의 크기를 5라고 정의했다(MAX_SIZE = 5), 크기가 5인 스택에 자료를 5개보다 더 추가하면 어떻게 될까?<br><br>
-> 스택의 크기를 초과해 새로운 자료를 추가하지 못하는 현상, 오버플로우(Overflow) 발생함

```c
void push(element item){                // 스택의 삽입 연산
    if(top >= SIZE - 1){
        printf("Stack is Full\n");
        return;
    }
    else
    stack[++top] = item;
}
```
***
## Pop()
- `Pop()` 연산은 스택에서 자료를 가져오는 연산이다<br>
-> 여기서 자료를 가져온다는 것은 스택에서 제거한 뒤 가져온다는 뜻도 포함이다
- `top`은 가장 최근 자료인 `B(인덱스 : 1)`를 가리키고 있다<br>
이 상태에서 Pop()연산을 수행하면 B가 제거되어 반환된다<br>
그 결과 스택에는 `A(인덱스 : 0)`만 남음
- 아무 자료가 없는 빈(Empty) 스택이 되었을 때, `Pop()`연산을 다시 수행하면 어떤 일이 발생할까?<br><br>
-> 아무런 자료가 없어 반환하지 못하는 현상, 언더 플로우(Underflow) 발생

```c
element pop(){                          // 스택의 삭제 연산
    if(top == -1){
        printf("Stack is Empty\n");
        return 0;
    }
    else
        return stack[top--];            // 반환 값은 top이 가리키는 값이고, top 포인터는 1 감소
}
```
***
## Peek()
- `Pop()연산`과 마찬가지로 스택의 가장 최근 자료를 반환하지만, 자료를 제거하지 않는다

```c
element peek(){                         // 스택의 조회 연산
    if(top == -1){
        printf("Stack is Empty\n");
        return 0;
    }
    else
        return stack[top];              // 반환값은 top이 가리키는 값이고, top 포인터는 변함 없음
}
```
***
# 큐(Queue)
- 먼저 들어온 데이터가 먼저 나가는 구조
- 리스트의 한 쪽 끝에서는 자료가 삽입되고 다른 한 쪽에서는 자료가 삭제된다
- 삽입이 발생하는 부분은 `rear(tail)`라는 포인터가 가리키며, 삭제가 발생하는 부분은 `front(head)`라는 포인터가 가리킨다
***
## 큐의 연산
- 큐의 연산에는 특별한 연산자는 없고, 자료를 큐에 삽입하고 삭제할 수 있다
- 자료를 큐에 삽입하기 위해서는 `rear` 포인터가 가리키는 위치보다 1 증가한 위치(rear + 1)에 삽입
- 자료를 큐에서 삭제하기 위해서는 `front` 포인터가 가리키는 위치보다 1 증가한 위치(front + 1)에서 삭제
- `front`와 `rear`의 초깃값은 -1이다
***
## 선형 큐와 원형 큐
### 선형 큐
- 정수를 저장할 수 있는 큐를 만드려면 먼저 정수의 1차원 배열을 정의하고 삽입, 삭제를 위한 변수인 `front`와 `rear`를 만든다
<br>데이터가 증가되면 `rear`를 하나 증가시키고 그 위치에 데이터가 저장된다<br>
삭제할 때는 `front`를 하나 증가시키고 `front`가 가리키는 위치에 있는 데이터를 삭제한다
- 선형 큐의 문제점 : `front`와 `rear`의 값이 계속 증가하기 때문에 언젠가는 배열의 끝에 도달하게 되고, 배열의 앞 부분이 비어 있더라도 사용하지 못한다<br>
따라서, 주기적으로 모든 요소들을 왼쪽으로 이동시켜야 한다
***

### 원형 큐
- 선형 큐의 문제점은 선형이 아니라 원형으로 생각하면 쉽게 해결된다<br> 즉, `front`와 `rear`의 값이 배열의 끝에 도달하면 다음에 증가되는 값은 0이 되도록 한다

#### 원형 큐의 삽입 삭제 구현
- 삽입, 삭제는 선형 큐와 같이 `rear`와 `front`가 가리키는 위치 +1에 삽입, 삭제한다
- `front`와 `rear`의 값이 같으면 원형 큐가 비어 있음을 나타낸다
- 원형 큐에서는 하나의 자리는 `포화(Full)`상태와 `공백(Empty)`상태 구별을 위해 항상 비워둔다

```c
#include <stdio.h>
#define MAX_SIZE 100

// 큐를 구조체 선언
typedef int element;
typedef struct{
    element queue[MAX_SIZE];
    int front, rear;
} QueueType;

// 포화 상태, 공백 상태 error 처리
void error(char *message){
    fprintf(stderr, "%s\n", message);
    exit(1);
}

// 초기화 함수
void init(QueueType *q){
    q->front = q->rear = 0;
}

// 삽입 함수
void enqueue(QueueType *q, element item){
    if((q->rear+1) % MAX_SIZE == q->front)      // 포화상태 점검
        error("Queue is Full");
    q->rear = (q->rear + 1) % MAX_SIZE;
    q->queue[q->rear] = item;
}

// 삭제 함수
element dequeue(QueueType *q){
    if(q->front == q->rear)
        error("Queue is Empty);
    q->front = (q->front + 1) % MAX_SIZE;
    return q->queue[q->front];
}
```
***
# 리스트(List)
## 선형 리스트
- 매우 간단하고 일반적인 데이터 구조이며 리스트의 원소들이 기억장치의 저장공간에 연속적으로 있다
- `장점` : 기억 장소의 활용도가 높으며, 자주 변하지 않는 데이터의 저장에 유리하다 <br>
`단점` : 삽입, 삭제 시에 데이터 이동 횟수가 많으며 여유분의 연속적 기억 장소를 필요로 한다
***
## 연결 리스트
- 자료를 기억하는 장소(Data Field) 이외에 다음 자료를 가리키는 포인터(Linked Field)를 두어 자료의 삽입, 삭제 시 자료의 이동을 최소화 할 수 있는 자료구조이다
- 연결리스트 구조를 표현하기 위해 하나의 원소를 기억하는 구조를 `노드(Node)`라 하며, 각 노드는 `Data Field`와 `Linked Field`로 구성된다
- `Data Field`부분에는 원소의 실제 값이 기억되며, `Linked Field`는 다른 자료가 저장되어 있는 주소인 포인터가 기억됨
- `Linked Field`가 하나인 연결 리스트를 `단순 연결 리스트(Single linked list)`라 하며, 이 `Linked Field`는 다음에 있는 자료를 가리키는 포인터가 기억된다
- `Linked Field`가 2개인 연결 리스트를 `이중 연결 리스트(double linked list)`라 하며, 각각 오른쪽(후행) 자료를 가리키는 포인터가, 왼쪽(선행) 자료를 가리키는 포인터가 기억된다.

- `장점` : 
    - 노드의 삽입과 삭제가 용이하다
    - 연속적인 기억 공간이 없어도 저장이 가능하다
- `단점` :
    - `Linked Field`의 사용으로 선형 리스트보다 많은 기억 공간을 필요로 한다
    - 알고리즘 구현이 복잡하다
    - 마지막 노드의 연결 부분에 `NULL`이 없거나 어떤 노드에서 포인터를 잃으면 다음 노드를 가리킬 수 없어서 특정 노드 검색 시 무한루프에 빠질 수 있다
***
### 단순 연결 리스트의 구현
- 구조체 정의
```c
typedef int element;
typedef struct ListNode{
    element data;               // Data Field : element 타입 데이터 저장
    struct ListNode *link;      // Linked Field : 현재 구조체를 가리키는 포인터 정의
}ListNode;
```
- 헤드 노드 생성
```c
ListNode *p1;                                   // 포인터 생성
p1 = (ListNode*)malloc(sizeof(ListNode));       // 노드 크기만큼 동적 메모리 할당
```
- 노드 생성
``` c
p1 -> data = 10;
p1 -> link = NULL;
```
***
### 단순 연결 리스트의 삽입 연산 구현
`void insert_node(ListNode *phead, ListNode *p, ListNode *new_node);`
- `*phead` : 헤드 포인터(head에 대한 포인터)
- `*p`    : 삽입될 위치의 앞 노드를 가리키는 포인터, 이 노드 다음에 삽입
- `*new_node` : 새로운 노드를 가리키는 포인터
<br><br>
- 실제 삽입을 구현할 때는 3가지 경우로 나누어 생각한다
1. head가 `NULL`인 경우
    - head가 NULL이라면 현재 삽입하려는 노드가 첫 번째 노드가 된다
    따라서 head의 값만 변경하면 된다
2. p가 `NULL`인 경우
    - 선행 노드 p가 `NULL`인 경우, 리스트의 맨 앞에 삽입한다
    먼저 `new_node`의 link가 head와 같은 값을 갖도록 하고 다음에 head가 `new_node`를 가리키도록 한다
3. head와 p가 `NULL`이 아닌 경우
    - 가장 일반적인 경우다. `new_node`의 link에 p->link 값을 복사한 뒤, p->link가 `new_node`를 가리키도록 한다

```c
// phead    : 리스트의 헤드 포인터
// p        : 선행 노드
// new_node : 삽입될 노드
void insert_node(ListNode *phead, ListNode *p, ListNode *new_node){
    if(phead == NULL){                  // 공백 리스트
        new_node -> link = NULL;
        phead = new_node;
    }
    else if(p == NULL){                 // p가 NULL
        new_node -> link = phead;
        phead = new_node;
    }
    else{
        new_node -> link = p -> link;
        p -> link = new_node;
    }
}
```
***
### 단순 연결 리스트의 삭제 연산 구현
`void remove_node(ListNode *phead, ListNode *p, ListNode *removed);`
- `*phead` : 헤드 포인터(head에 대한 포인터)
- `*p`     : 삭제 될 노드의 앞 노드를 가리키는 포인터
- `*removed` : 삭제 될 노드를 가리키는 포인터

1. p가 `NULL`인 경우
    - 연결 리스트의 첫 번째 노드를 삭제한다
    - 헤드 포인터를 변경하고 `removed` 노드가 차지하고 있는 공간을 시스템에 반환한다

2. p가 `NULL`이 아닌 경우
- `removed` 앞의 노드인 p의 링크가 `removed` 다음 노드를 가리키도록 한다
- `removed` 노드가 차지하고 있는 공간을 시스템에 반환한다

```c
void remove_node(ListNode *phead, ListNode *p, ListNode *removed){
    if (p == NULL)
        phead = phead -> link;
    else
        p -> link = removed -> link;
    
    free(removed);
}
```