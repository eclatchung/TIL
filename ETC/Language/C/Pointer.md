# Pointer

C언어 포인터 관련 모르는 거 추가

## typedef
- 자료형을 재정의 하고 짧고 쉬운 이름을 사용가능
```C
//1.
struct student{
	int num;
	double grade;
}

typedef struct student Student; //struct student를 Student 로 재정의 

//2.
typedef struct (student) // student 생략가능
{	int num;
	double grade;
}Student;

```

`1`과 `2`는 같은 내용이다.

## 구조체 포인터

```C
typedef struct student{
	int num;
	double grade;
}Student;

Student yuni = {1,100.0};
Student *ps = &yuni;


printf((*ps).num); // 1;
printf(ps->num); // 1;

```

`ps` : 구조체 포인터
`num` : 구조체 변수의 멤버