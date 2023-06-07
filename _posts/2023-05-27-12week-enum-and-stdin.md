---
title: "12week-enum-and-stdin"
date: 2023-05-27 13:58
description: "C언실 12주차 과제중 enum과 stdin의 버퍼"
categories: [Blog, writing]
tags: [tag]     #lowercase
author: me
#math: true
#pin: true
#img_path: /imgs/
#mermaid: true

---

[C에서 enum과 C++에서 enum는 다르다. : 네이버 블로그](https://blog.naver.com/chhh92/220529074379)`
```c
enum days {SUN, MON, TUE, WED, THU, FRI, SAT};
enum days day;

day = SUN;
day = 2;
```

C에서는 4, 5번줄 둘다 성공, C++에서는 5번줄 에러.

  

위 소스를 C로 해석하면
day 변수 자료형은 int 이고 enum days에 정의된 상수들의 자료형은 int 이다.

4, 5번 대입되는 상수가 모두 정수 범위에 속하므로 에러가 발생하지 않는다. (enum days의 범위 0~6 외의 정수도 대입된다.)

C++로 해석하면

day 변수 자료형은 days(enum days에 enum 생략) 이고, days에 정의된 상수들의 자료형은 int 이다.

4, 5번에 대입되는 상수의 자료형은 4번줄은 days, 5번줄은 정수이기때문에 4번줄은 성공하고 5번줄은 문법적 에러(잘못된 형변환)가 발생한다.

  

추가로, enum은 C에서는 int로 취급되기 때문에 enum 변수로 연산이 가능하지만, C++에서 enum은 enum 자료형으로 취급되기 때문에 기본연산은 불가능하고, 클래스로 만들어 operator overloading을 해야 연산이 가능하다.

  

공통적인것은 enum에 정의된 상수들의 자료형은 int로 취급 되는것인데, C언어는 오로지 int만, C++은 enum자료형로 취급하면서 int도 취급해준다.

때문에 enum상수를 int로써 사용한다면 C나 C++나 같다.

  

day 변수가 출력될때는 정수로 출력되고

days에서 정의한 상수들을 다른 정수 변수에 대입되고

days변수가 정수 변수에 대입이 된다.

하지만 days변수에 다른 enum 상수는 대입은 상수가 enum 자료형로써 취급되기 때문에 형변환 요류가 발생한다.


```c
void ReadLine(char temp[]){
	fgets(temp,MAXLEN,stdin);//한줄 읽기
	temp[strlen(temp)-1] = '\0';//개행 지우기
}
```

```c
while(getchar() != '\n');//버퍼 지우기
```

[❌ fflush(stdin), rewind(stdin) ❌](https://www.acmicpc.net/blog/view/108)
[씹어먹는 C 언어 - <15 - 2. 일로와봐, 문자열(string) - 버퍼에 관한 이해>](https://modoocode.com/32) 
`scanf()`는 `' ', '\t', '\n'`를 만날 때 까지 `stdin`으로부터 데이터를 받아오게 됨

`fflush(stdin)`는 비표준 C문법, MSVC 2015 이후에는 지원하지 않음

`scanf(" %c", &c);`
`scanf`의 형식 문자열 `" "`은 '공백문자가 아닌 글자가 나올 때 까지 읽고, 읽은 공백문자는 그냥 버려라' 라는 의미를 가지고 있습니다. 즉, 이 프로그램에서 `a` 를 읽기 전에 있을 수 있는 개행문자는 형식 문자열 `" "` 가 담당합니다

버퍼 문제가 생기는 이유
일반적인 `scanf()` 는 앞의 공백을 제외하고 받지만, %c는 공백도 입력도 받게 됨
`scanf()`는 데이터 뒤의 공백을 처리하지 않으므로 버퍼에 남아있는 공백이 %c로 들어갈 수 있음

함수원형 : `char* fgets(char* str, int num, FILE* pFile);`

파일에서 부터 string(=문자열)을 get 가지고 옵니다.
즉, 파일로 부터 문자열을 가지고 오는 함수입니다.

: 함수설명
첫번째 인자 : 파일에서 부터 가지고 온 문자열을 넣는 변수 입니다. 문자열을 가리키는 캐릭터 타입의 포인터
두번째 인자 : 한번에 가지고올 문자열의 길이를 넣는 변수 입니다.
세번째 인자 : 파일의 파일 포인터를 집어 넣습니다.
반환형 : 가지고 온 문자열을 반환하거나, 파일의 끝에 도달했을때는 널 포인터 반환.

: 함수동작
파일에 아래와같이 세줄이 있다고 할때 fgets 함수는 문자열 끝에있는 "\n" 띄어쓰기를 기준으로하거나 두번째 매개변수로 집어 넣은 num-1 개의 문자열을 기준으로 으로 문자열을 판단해서 가지고 옵니다. 
num-1 : `'\0'`을 집으로
즉. num-1 보다 작은데 \n이 나오면 해당 문자열까지만 읽음
num-1 까지 읽었을때 \n이 없더라도 num-1 까지만 읽음.
읽을게 없을때는 null 포인터를 반환