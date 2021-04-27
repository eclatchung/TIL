# 연결 리스트

## 리스트
- 데이터를 나란히 저장
- 중복된 데이터의 저장을 막지 않음
- 구현 방식에 따른 구분
	- [순차리스트](순차리스트) : 배열을 기반으로 구현된 리스트
	- [연결리스트](연결리스트) : 메모리의 동적 할당을 기반으로 구현된 리스트

## 추상자료형 ADT
**void ListInit(List *plist)**
	- 초기화할 리스트의 주소값을 인자로 전달
	- 리스트 생성후 제일 먼저 호출되어야 하는 함수
**void LInsert(List *plist, LData data)**
	- 리스트에 data를 저장
**int LFirst(List *plist, LData *pdata)**
	- 첫번째 데이터가 pdata다 가리키는 메모리에 저장
	- 데이터의 참조를 위한 초기화가 진행됨
	- 참조 성공시 TRUE(1), 실패시 FALSE(0) 반환
**int LNext(List *plist, LData *pdata)**
	- 참조된 데이터의 다음 데이터가 pdata가 가리키는 메모리에 저장
	- 순차적인 참조를 위하여 반복호출이 가능
	- 참조를 새로 시작하려면 먼저 LFirst 함수 호출
	- 참조 성공시 TRUE(1), 실패시 FALSE(0) 반환
**LData LRemove(List * plist)**
	- LFirst 또는 LNext 함수의 마지막 반환 데이터 삭제
	- 삭제된 데이터는 반환
	- 마지막 반환 데이터를 삭제하므로 연이은 반복 호출은 허용하지 않음
**int LCount (List * plist)**
	- 리스트에 저장되어있는 데이터 수를 반환

## 순차리스트 
```C
#define ListLen 100
#define TRUE 1
#define FALSE 0

typedef struct __ArrayList{
	LData arr[ListLen];
	int numOfData;
	int curPosition;
}ArrayList
```

### 초기화
```C
void ListInit(List *plist){
	(plist -> numOfData) = 0; // 저장된 데이터의 수 초기화
	(plist -> curPosition) = -1; // 현재 데이터 참조 위치 초기화
}
```

### 리스트 삽입
```C
void LInsert (List *plist LData data){
	if(plist -> numOfData >= LIST_LEN) // 1. 리스트가 리스트가 수용할 수 있는 공간이 있는지 확인 TRUE시에 공간 없으므로 반환;
	{	puts("저장 X"); return; }

	plist-> arr[plist->numOfData] = data; // 2. 데이터를 삽입
	(plist -> numOfData)++;// 3. 리스트가 가진 요소의 수 더함.

	return;
}
```

### 조회
#### 첫번째 조회
```C
int LFirst(List *plist, LData *pdata){
	if(plist-> numOfData == 0) // 리스트가 빈 리스트일때
		return FALSE;

	(plist -> curPosition) = 0; // 참조 위치 초기화
	*pdata = plist -> arr[0]; // 첫요소를 pdata에게 넘겨줌
	
	return TRUE;
}
```
#### 두번째 조회
```C
int LNext(List *plist, LData *pdata){
	if(plist-> curPosition >= (plist -> numOfData) -1 )
	// (plist -> numOfData)-1은 인덱스 끝번호, 더이상 참조하 데이터가 없는지 확인
		return FALSE;

	(plist-> curPosition)++; // 다음 원소를 참조하기 위해서 참조위치 ++함
	*pdata = plist -> arr[ plist-> curPosition];// 해당 요소를 pdata에게 넘겨줌

	return TRUE;
}
```
#### LFirst에서 curPosition을 초기화하고 증가 안시키는 이유
- LFirst 사용시 재설정이 되어 처음부터 사용가능하게 하기위해서.

### 삭제
LRemove함수가 호출되면 리스트의 멤버 curPosition을 확인해서, 조회가 이뤄진 데이터의 위치를 확인한 다음 삭제 ⇒ 중간 삭제시에 뒤에 저장된 데이터들이 한칸씩 이동 시켜서 그 빈공간을 채워야 한다.
```C
LData LRmove(List *plist){
	int rpos = plist -> curPosition;
	int num = plist -> numOfData;
	int i;
	LData rdata = plist -> arr[rpos];

	//삭제를 위한 데이터 이동을 진행하는 부분
	for(i = rpos; i <num -1; i ++)
		plist -> arr[i] = plist -> arr[i +1];

	(plist -> numOfData)--;
	(plist -> curPosition)--; // LNext사용시 현재 삭제된 자리의 새로운 LData가 참조되기 때문
	return rdata;
}
```

### 배열기반 리스트의 단점과 장점
- 장점
	- 데이터 참조가 쉬움
- 단점
	- 배열 길이가 초반에 결정되어야함 ( 메모리 특성이 정적)
	- 삭제의 과정에서 데이터의 이동이(복사)가 빈번함.

## 연결리스트
- [단순연결리스트](단순 연결리스트)
- [원형연결리스트](원형 연결리스트 )
- [양방향연결리스트](양방향 연결리스트)

## 단순 연결리스트
- 더미노드(DMY; dummy Node) 존재
	- 유효한 데이터를 지니지 않는 그냥 빈 노드
	- 넣은 이유 :  처음 추가되는 노드가 구조상 2번째 노드가 됨으로 노드의 추가, 삭제 및 조회의과정이 일괄됨
### 정렬기준이 추가된 리스트 자료구조의 ADT
- 연결리스트 ADT 와 동일
- void setSortRule(List *plist, int(*comp)(LData d1, LData d2)) 추가
**void setSortRule(List *plist, int(*comp)(LData d1, LData d2))**
	- 리스트에 정렬 기준이 되는 함수 등록

### 새 노드 추가시 리스트 머리(HEAD)와 꼬리(TAIL) 중 어디에 저장해야할까?
`HEAD` :  가장 먼저 시작하는 노드를 가리키는 포인터 변수 
	- 장점
		- `TAIL`불필요
	- 단점
		- 저장된 순서 유지가 안됨  
			- 역순으로 저장이됨 
			- 넣은 순서 1,2,3 ⇒ 저장된 순서 3 ,2, 1
`TAIL `:  리스트의 꼬리를 가리키는 포인터 변수
	- 장점
		- 저장된 순서가 유지됨 
	- 단점
		- `TAIL`필요

```C

typedef struct _node{
	LData data;
	struct _node *next;
} Node;

typedef struct _linkedList{
	Node * head;
	Node * cur;
	Node * before;
	int numOfData;
	int (*comp)(LData d1, Ldata d2); // 리스트의 정렬 기준이 되는 함수
} LinkedList;

```

### 초기화
```c
void ListInit(List * plist){
	plist -> head = (Node *)malloc(sizeof(Node)); // HEAD 에 더미 노드 생성
	plist -> head -> next = NULL;
	plist -> comp = NULL;
	plist -> numOfData = 0;
}
```

### 정렬 순서 함수 지정하기
```c
void SetSortRule(List *plist, int(*comp)(LData d1, LData d2)){
	plist -> comp = comp;
}
```
#### 정렬 함수 예시
```c
int whoIsPreced(Ldata d1, Ldata d2){
	if(d1 < d2){
		return 0; // d1 이 head에 가까움
	}
	if(d2 < d1){
		return 1; // d2가 head에 가까움
	}
}
```
- return 0;
	- head ——  D1 —— D2 —— tail;
- return 1;
	- head ——— D2 ——— D1 ——tail;   

### 데이터 삽입
```C
 void LInsert(List *plist, Ldata data){
	if(plist-> comp == NULL) // 정렬 기준이 없을시
		FInsert(plist, data); // HEAD에 노드 추가
	else  // 정렬 기준에 따라 삽입
		SInsert(plist,data);
}
```
#### FINSERT
```C
void FInsert (List *plist, LData data){
	Node * newNode = (Node *)malloc(sizeof(Node));
	newNode -> data = data;

	newNode -> next = plist -> head -> next;
	plist -> head -> next = newNode;

	(plist -> numOfData)++;
}
```
#### SINSERT
```C
void SInsert(List *plist, LData data){
	Node *newNode = (Node*)malloc(sizeof(Node));
	Node * pred = plist -> head; // 더미 노드

	newNode -> data = data;
	
	while(pred-> next != NULL && plist -> comp(data, pred -> next-> data) != 0){
		pred = pred -> next; // 다음 노드로 이동
}

	newNode -> next = pred -> next;
	pred -> next = newNode;

	(plist -> numOfData) ++;
}
```
##### `while(pred-> next != NULL && plist -> comp(data, pred -> next-> data) != 0)`
- 새 노드가 들어갈 위치를 찾는 반복문
	- 조건 1 : `pred -> next ≠NULL`
		- 마지막 노드인가 확인
	- 조건 2 : `plist -> comp(data, pred→ next→ data ≠0)`
		- 우선순위 비교하는 함수 호출
		- comp 
			- return 0
				- 첫번째 인자가 HEAD에 가까움
			- return 1;
				- 두번째 인자가 HEAD에 가까움


### 조회
#### LFirst : 첫번째 노드 ( DMY제외한 첫번째 노드) 값 조회하기
```C
int LFirst(List *plist, Ldata *pdata){
	if(plist -> head -> next == NULL)//DMY 다음에 NULL 값이면 갑싱 없음
		return FALSE;

	plist -> before = plist -> head; //DMY를 가리킴
	plist cur = plist -> head -> next; //DMY 이후의 첫번째 노드 값
	
	*pdata = plist -> cur -> data;
	return TRUE;
}
```
#### LNext
```C
int LNext(List *plist LData data){
	if(plist -> cur -> next == NULL)
		return FALSE;
	
	plist -> before = plist -> cur;
	plist -> cur = plist -> cur -> next;

	*pdata = plist -> cur -> data;
	return TRUE;
}
```

### 삭제
바로 이전에 호출된 LFirst or LNext 함수가 반환 데이터 삭제 ( cur 이 가리키는 값삭제)
- `before`는 움직이지 않음
	- 어짜피 `before`는 다시 `cur`의 자리를 가리키므로(원위치) 재조정 필요없음
```C
LData LRemove(List *plist){
	Node *rpos = plist -> cur;
	LData rdata = rpos ->data;

	plist -> before-> next = plist -> cur -> next;
	pllist -> cur = plist -> before;

	free(rpos);
	(plist -> numOfData)--;
	return rdata;
}
```

## 원형 연결리스트 
- 원형 연결 리스트에서는 머리와 꼬리의 구분이 없음
- 단순 연결리스트처럼 머리와 꼬리를 가리키는 포인터 변수를 각각 두지 않아도, 하나의 포인터 변수만 있어도 머리 또는 꼬리에 노드를 간단히 추가가능 
	- `tail`만 사용시 
		- TAIL :  `tail`
		- HEAD : `tail -> next`
- `LNext`기능이 무한 반복 호출이 가능해짐 -> 리스트 끝 도달시 첫번째 노드 부터 다시 조회
```c
typedef struct _node {
	Data data;
	struct _node * next;
} Node;

typedef struct _CLL{
	Node * tail;
	Node * cur;
	Node * before;
	int numOfData;
} CList;

```

### 초기화
```C
void ListInit(List *plist){
	plist -> tail = NULL;
	plist -> curr = NULL;
	plist -> before  = NULL;
	plist -> numOfData = 0; 
}
```

### 데이터 삽입
#### 머리에 추가 
```C
void LInsetFront(List *plist, Data data){
	Node *newNode = (Node *)malloc(sizceof(Node));
	newNode -> data = data;

	if(plist -> tail ==NULL){
		plist -> tail = newNode;
		newNode -> next = newNode;
	} else{
		newNode -> next = plist -> tail -> next;
		plist -> tail -> next = newNode ;
	}
	(plist->numOfData)++;
}
```
#### 꼬리에 추가 
``` C
void LInsrt(List *plist, Data data){
	Node *newNode = (Node*)malloc(sizeof(Node));
	newNode -> data = data;

	if(plist -> tail == NULL){
		plist -> tail = newNode;
		newNode -> next = newNode;
	} else{
		newNode -> next = plist -> tail -> next;
		plist -> tail -> next = newNode;
		plist -> tail = newNode;
	}

	(plist -> numOfData)++;
}
```

### 조회
#### LFirst
```C
int LFirst(List *plist, Data *pdata){
	if(plist -> tail == NULL)
		return FALSE;

	plist -> before = plist -> tail;
	plist -> cur = plist -> tail -> next; 

	*pdata = plist -> cur -> data;
	return TRUE;
}
```
#### LNext
```C
int LNext(List *plist, Data *pdata){
	if(plist-> tail == NULL)
		return FALSE;

	plist -> before = plist-> cur;
	plist -> cur = plist -> cur -> next;

	*pdata = plist -> cur -> data;

	return TRUE;
}
```

### 삭제
- 삭제할 노드의 이전 노드가, 삭제할 노드의 다음 노드를 가리키게 한다.
- `cur`을 한칸 뒤로 이동
- 기존 LRemove 와 다른 예외상황
	- 삭제할 Node를 `TAIL`이 가리키는 경우
		- ⇒ 삭제될 NODE의 이전 NODE(`before`)를 `TAIL`이 가리켜야함.
	- 삭제할 NODE 가 리스트에 홀로 남겨진 경우
		-  ⇒ `TAIL`이 NULL 가리켜야함.
```C
LData LRemove(List *plist){
	Node *rpos = plist -> cur;
	Data rdata = rpos -> data;

 	if(rpos == plist -> tail){
		if(plist -> tail == plist -> tail -> next)
			plist -> tail = NULL;
		else 
			plist -> tail = plist -> before;
	}
	
	plist -> before -> next = plist -> cur -> next;
	plist -> cur = plist -> before;

	free(rpos);
	(plist -> numOfData)--;
	return rdata;
}
```

## 양방향 연결리스트
- 포인터 변수 `before`는 양방향 리스트에서는 사용안함
	- `before`는 원형 리스트에서 삭제의 과정을 위해서 필요 ⇒ 일방적으로 한방향으로 움직이기 때문
- DMY 없는 버전
```c
typedef struct _node {
	Data data;
	struct _node * next;
	struct _node * prev;
} Node;

typedef struct _dbLinkedList{
	Node * head;
	Node * cur;
	int numOfData;
} DBLinkedList;

```

### 초기화
```C
void ListInit(List *plist){
	plist -> head = NULL;
	plist -> numOfData = 0;
}
```

### 데이터 삽입
```C

void LInsert(List *plist, Data data){
	Node *newNode = (Node*)malloc(sizeof(Node));
	newNode -> data = data;

	newNode -> next = plist -> head;
	
	if(plist -> head != NULL) ->두번째 삽입이후
		plist -> head -> prev = newNode;

	newNode -> prev = NULL;
	plist -> head = newNode;

	(plist -> numOfData)++;
}
```

### 조회
- LFirst
- LNext
- LPrevious
#### LFirst
```C
int LFirst(List *plist, Data *pdata){
	if(plist -> head == NULL)
		return FALSE;

	plist -> cur = plist -> head;
	*pdata = plist -> cur -> data;
	return TRUE;
}
```
#### LNext
```C
int LNext(List *plist, Data *pdata){
	if(plist -> cur -> next == NULL)
		return FALSE;

	plist -> cur = plist -> cur -> next;
	*pdat = plist-> cur ->data;
	return TRUE;
}
```
#### LPrevious
```C
int LPrevious(List *plist, Data *pdata){
	if(plist -> cur -> prev ==NULL)
		return FALSE;

	plist -> cur = plist -> cur -> prev;
	*pdata = plist -> cur -> data;
	return TRUE;
}
```
