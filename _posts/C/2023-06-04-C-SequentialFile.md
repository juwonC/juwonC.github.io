---
title: "[C]순차 파일 처리"
excerpt: "순차 파일 처리"

categories:
  - C
tags:
  - [C, 순차 파일 처리]

toc: true
toc_sticky: true

date: 2023-06-04
---

## 📚순차 파일 처리
정보의 집합을 파일이라고 하면 파일은 논리적으로 레코드 단위로 이뤄지며 레코드는 필드로 구성되어 있습니다. 즉 필드가 모여서 레코드를 이루고 레코드가 모여서 파일을 구성합니다.

컴퓨터가 자료를 파일로 입출력 작업을 처리 할 때 사용되는 논리적인 기본 단위는 레코드입니다. 자료의 특성상 레코드 길이가 일정한 경우와 일정하지 않은 경우가 있습니다. 레코드의 길이가 일정하지 않은 파일을 순차 파일이라고 하고 레코드의 길이가 일정한 파일을 랜덤 파일이라고 합니다. 따라서 레코드가 일정하지 않은 순차 파일에서 일정하지 않은 레코드를 구별해줄 필요가 있습니다. 순차 파일의 레코드 구분 기호는 CR과 LF가 사용됩니다.

순차 파일에서 레코드를 파일에 쓸 때 \n 기호를 CR/LF로 바꿔서 기록하고 읽을 때는 CR/LF를 \n 기호로 바꿔서 읽게 됩니다. 이런 과정을 거치는 파일 모드를 텍스트 모드라고 합니다. 텍스트 모드로 파일을 열고 기록할 때 \n 문자를 반드시 레코드와 레코드 사이에 삽입하고, 읽을 때는 CR/LF까지 한꺼번에 읽어 내는 것이 좋습니다. 순차 파일은 기록할 때 순차적으로 기록되고 읽을 때 순차적으로 읽히는 파일을 말합니다.

<br>

### 📄순차 파일 만들기

* **putc()** 함수
<br>

```c
putc(c, fp);
// fp가 가리키는 파일에 c에 있는 문자를 출력
```

putc() 함수는 문자 단위의 파일 출력함수로 지정된 파일로 한 문자를 출력합니다. 출력 후 파일 포인터의 위치는 1만큼 증가하게 됩니다. putc() 함수는 호출이 성공하면 출력된 문자를 반환하고, 에러가 발생했다면 EOF(-1)값을 반환합니다.

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	char c;

	// sample.txt 파일을 쓰기 모드로 개방
	fp = fopen("sample.txt", "w");

	// 파일 개방 에러 체크
	if (fp == NULL)
	{
		printf("파일을 개방할 수 없습니다!");
		exit(1);
	}

	printf("문자열을 입력하시오. 입력을 끝내려면 Ctrl + z를 누르시오. \n");

	// 문자 출력의 끝을 판별
	while ((c = getchar()) != EOF)
	{
		// 문자를 파일로 출력
		putc(c, fp);
	}

	// 파일 닫기
	fclose(fp);
}
```

<br><br>

* **fputs()** 함수
<br>

```c
fputs(s, fp);
// 지정된 파일에 문자열을 출력
```

fputs() 함수는 문자열을 파일로 출력할 때 많이 쓰이는 함수입니다. fputs() 함수는 호출이 성공적이라면 음이 아닌 값을 반환하고 에러가 발생하면 EOF(-1) 값을 반환합니다.

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	char name[64];

	// sample.txt 파일을 쓰기 모드로 개방
	// 파일 개방 에러 체크
	if ((fp = fopen("sample.txt", "w")) == NULL)
	{
		puts("파일을 개방할 수 없습니다!");
		exit(1);
	}

	printf("이름을 입력하시오. 입력을 끝내려면 'end'를 입력하시오. \n");
	gets(name);

	// 입력된 문자열이 end가 아닐 동안 loop
	while (strcmp(name, "end"))
	{
		// 하나의 문자열에 다른 것("\n")을 추가하는 문자열 조작 함수
		strcat(name, "\n");

		// 문자열을 fp가 가리키는 파일에 출력
		fputs(name, fp);
		gets(name);
	}

	// 파일 닫기
	fclose(fp);
}
```

<br><br>

* **fprintf()** 함수

```c
fprintf(fp, "%s %d \n", a, b);
// 지정된 형식대로 자료를 파일 포인터 변수가 가리키는 곳에 출력
```

fprintf() 함수는 지정된 형식을 가지고 파일에 자료를 출력함으로서 새로운 파일을 생성하는 함수입니다. 숫자, 문자 등 복합적인 자료로 구성된 레코드를 저장할 때 유용한 함수입니다. fprintf() 함수는 호출이 성공적일 때 출력된 문자의 수를 반환하고 오류가 발생하면 음수가 반환됩니다.

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	char num[10], name[10];
	int mid, term, rep, att;

	// sample.txt 파일을 쓰기 모드로 개방
	// 파일 개방 에러 체크
	if ((fp = fopen("sample.txt", "w")) == NULL)
	{
		printf("파일을 개방할 수 없습니다!");
		exit(1);
	}

	// 화면으로 문자열 출력, stdout-모니터를 가리키는 특수한 파일 포인터
	fprintf(stdout, "학번 이름 중간 기말 레포트 출석 점수를 입력 \n");
	
	for (int i = 0; i < 5; ++i)
	{
		scanf("%s %s %d %d %d %d", num, name, &mid, &term, &rep, &att);

		// 지정된 출력 형식으로 자료를 파일에 출력
		fprintf(fp, "%-10s %-8s %3d %3d %3d %3d \n", num, name, mid, term, rep, att);
	}

	// 파일 닫기
	fclose(fp);
}
```

<br><br>

### 📄순차 파일 읽기

* **getc()** 함수
<br>

```c
getc(fp);
// 지정된 파일로부터 한 문자를 읽어 온다
```

getc() 함수는 파일 포이터를 갖는다는 것만 제외하면 표준입력함수 getchar()와 유사하지만 getchar()는 표준입력 장치로만 입력받기 때문에 입력 위치를 명시하지 않아도 되지만, getc()는 파일을 다루는 함수라서 사용하는 파일의 위치를 파일 포인터로 명시해야 합니다. getc()는 지정된 파일 포인터 fp로부터 한 문자를 읽어 오고 한 문자를 읽어 온 후에는 파일 포인터가 자동으로 +1 증가하여 다음 문자를 가리킵니다. 파일 끝을 만나거나 에러가 발생하면 EOF(-1) 값을 반환합니다.

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	char c;

	// sample.txt 파일을 읽기 모드로 개방
	// 파일 개방 에러 체크
	if ((fp = fopen("sample.txt", "r")) == NULL)
	{
		printf("파일을 개방할 수 없습니다!");
		exit(1);
	}

	// getc() 함수에 의해 한 문자씩 읽어와 c에 전달
	while ((c = getc(fp)) != EOF)
	{
		putchar(c);
	}

	// 파일 닫기
	fclose(fp);
}
```

<br><br>

* **fgets()** 함수
<br>

```c
fgets(s, 문자열 길이 + 1, fp);
/* 지정된 파일로부터 해당 문자열 길이 만큼의 
 문자를 읽어와 문자열 변수에 저장 */
```

fgets() 함수는 파일에 저장된 문자열 자료를 읽을 때 사용되는데 읽어 낼 문자열의 길이를 반드시 명시해야 합니다. 끝을 알리는 제어문자 CR/LF는 '\n'로 변환되어 출력되고 마지막에 '\0'이 추가됩니다. 파일 끝을 만나거나 에러가 발생하면 null 값을 반환합니다.

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	char name[64];

	// sample.txt 파일을 읽기 모드로 개방
	// 파일 개방 에러 체크
	if ((fp = fopen("sample.txt", "r")) == NULL)
	{
		printf("파일을 개방할 수 없습니다!");
		exit(1);
	}

	while ((fgets(name, 20, fp) != NULL))
	{
		printf("%s", name);
	}

	// 파일 닫기
	fclose(fp);
}
```

<br><br>

* **fscanf()** 함수
<br>

```c
fscanf(fp, "%s %d", &a, &b);
/* 파일 포인터가 가리키는 곳으로부터
 지정된 형식대로 자료를 읽어 온다 */
```

fscanf() 함수는 숫자, 문자 등 여러 항목의 복합적인 자료로 구성된 레코드를 읽을 때 유용한 함수입니다. 파일 포인터가 파일 끝을 만나거나 에러가 발생하면 EOF(-1)을 반환합니다. 파일 끝을 판별하는데 feof() 함수를 함께 사용하는데 이 함수는 파일 끝에 도달하면 0이 아닌 값을 반환합니다.

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	char num[10], name[10];
	int mid, term, rep, att;

	// sample.txt 파일을 쓰기 모드로 개방
	// 파일 개방 에러 체크
	if ((fp = fopen("sample.txt", "w")) == NULL)
	{
		printf("파일을 개방할 수 없습니다!");
		exit(1);
	}

	printf("학번		이름	중간 기말 레포트 출석 \n");

	// 파일 끝 검사를 위해 feof() 함수 사용, 0인 동안 loop
	while (!feof(fp))
	{
		// 파일에 저장된 자료의 형식에 맞게 입력 형식을 지정
		fscanf(fp, "%10s %8s %4d %4d %4d %4d \n", num, name, &mid, &term, &rep, &att);

		// 화면에 출력하기 위해 출력 형식 지정
		printf("%-10s %-8s %4d %4d %4d %4d \n", num, name, mid, term, rep, att);
	}

	// 파일 닫기
	fclose(fp);
}
```

<br><br>

### 📄순차 파일의 레코드 추가
이미 저장된 순차 파일의 끝에 새로운 레코드를 추가해야 할 때는 파일 개방 모드만 변경 해주면 됩니다.

레코드를 추가하기 위해 파일을 열게 되면 파일이 없어도 상관없습니다. 파일이 존재한다면 그 파일 끝에 레코드를 추가로 삽입시키지만 만약 파일이 없다면 그 파일 이름으로 새로운 파일을 자동으로 생성시킵니다.

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	
	fp = fopen("sample.txt", "a");
	fputs("KIM \n", fp);
	fputs("PARK \n", fp);
	fputs("CHOI \n", fp);

	fclose(fp);
}
```

<br><br><br>

## 📚램덤 파일 처리
고정 길이 레코드를 갖고 있는 랜덤 파일은 가변 길이 레코드를 갖고 있는 순차 파일에 비해 어느 정도의 기억 공간을 낭비하지만 고정 길이 레코드를 사용하면 레코드의 검색이 빠르고 효율적으로 이뤄지는 장점이 있습니다.

<br>

### 📄랜덤 파일 열기
랜덤 파일을 입출력하려면 2진 모드로 파일을 개방하는 것이 좋습니다. 레코드 구분을 위해 CR/LF 신호가 필요 없기 때문에 변환 작업을 하지 않는 2진 모드가 사용됩니다.

2진 파일은 텍스트 파일보다 적은 기억공간을 차지한다는 장점이 있습니다. 하지만 어떤 프로그램에서는 파일을 읽어 들일 수 없다는 단점이 있습니다. 오직 2진 파일에 접근할 수 있도록 작성된 C 프로그램만 읽고 쓸 수 있습니다.

2진 모드에서 레코드 길이는 프로그래머가 결정해야 합니다. 랜덤 파일에서는 레코드 길이가 일정하고 레코드의 길이을 알고 있기 때문에 파일 포인터를 레코드의 앞뒤로 마음대로 옮기면서 입출력을 수행할 수 있습니다.

<br><br>

### 📄랜덤 파일 만들기

* **fwrite()** 함수
<br>

```c
fwrite(저장 자료 변수, 레코드 길이, 레코드 개수, 파일 포인터);
```

fwrite() 함수는 텍스트 파일을 저장할 때 사용하지만 주로 랜덤 파일을 처리할 때 많이 사용합니다. 텍스트 모드에서 null 값을 쓰거나 읽을 수 없지만 2진 모드에서 null 값을 포함한 자료를 입출력할 수 있습니다.

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	char name[10];

	// 파일을 2진 파일 쓰기 모드로 개방
	if ((fp = fopen("sample.dat", "wb")) == NULL)
	{
		puts("파일을 개방할 수 없습니다!");
		exit(1);
	}

	printf("이름을 입력하시오. 입력을 끝내려면 'end'를 입력하시오. \n");
	gets(name);

	// 입력 문자열이 end가 아닐 동안 loop
	while (strcmp(name, "end"))
	{
		// 2진 파일에 쓰기
		fwrite(name, 10, 1, fp);
		gets(name);
	}

	fclose(fp);
}
```

<br><br>

### 📄랜덤 파일 읽기

* **fread()** 함수
<br>

```c
fread(읽을 자료 변수, 레코드 길이, 레코드 개수, 파일 포인터);
```

fread() 함수는 읽기에 성공하면 읽은 레코드 수를 반환하고 실패하거나 파일 끝을 만나면 다른 값을 반환합니다.

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#pragma warning(disable:4996)

void main()
{
	FILE* fp;
	char name[10];

	// 파일을 2진 파일 읽기 모드로 개방
	if ((fp = fopen("sample.dat", "rb")) == NULL)
	{
		puts("파일을 개방할 수 없습니다!");
		exit(1);
	}

	// 입력 문자열이 end가 아닐 동안 loop
	while (1)
	{
		// 레코드 개수가 1이므로 1이 아닌 값이 리턴되면 while문 벗어남
		if (fread(name, 10, 1, fp) != 1)
		{
			break;
		}

		puts(name);
	}

	fclose(fp);
}
```

<br><br>

### 📄랜덤 파일의 위치 제어

* **fseek()** 함수
<br>

```c
fseek(파일 포인터 변수, 이동할 상대 위치, 기준 위치를 지정하는 모드);
```

fseek() 함수는 파일 포인터를 임의의 위치로 이동시키는 함수입니다. 이 함수를 이용하면 랜덤 파일의 특정 부분을 입출력할 수 있게 합니다. 파일에서 현재 읽어 들일 위치를 가리키는 파일 위치 지시자를 조작하여 임의의 위치로 접근합니다.

이동할 상대 위치는 건너띄고 싶은 바이트의 수를 나타냅니다. + 값은 순방향, - 값은 역방향으로 이동하는 것을 의미합니다.

<br>

| 기준 위치 모드 | 동일 기호 | 설명 |
| :---: | :---: | :---: |
| 0 | SEEK_SET | 파일의 시작 위치 |
| 1 | SEEK_CUR | 현재 파일 포인터의 위치 |
| 2 | SEEK_END | 파일의 끝 위치 |

<br>

```c
#include <stdio.h>
#include <stdlib.h>
#pragma warning(disable:4996)

void main()
{
	char str[10];

	FILE* fp = fopen("sample.txt", "wt");
	fputs("1234567890", fp);
	fclose(fp);

	fp = fopen("sample.txt", "rt");
	fseek(fp, 7, SEEK_SET);
	fgets(str, 4, fp);
	printf("7번째부터 3글자 출력 :  %s \n", str);

	fseek(fp, -2, SEEK_CUR);
	fgets(str, 3, fp);
	printf("현재 위치에서 앞의 2글자부터 2글자 출력 :  %s \n", str);

	fseek(fp, -9, SEEK_END);
	fgets(str, 6, fp);
	printf("맨 뒤에서 9번째 앞부터 5글자 출력 :  %s \n", str);

	fclose(fp);
}
```

<br><br>

* **ftell()** 함수
<br>

```c
ftell(파일 포이터 변수);
```

ftell() 함수는 현재 파일 위치 지시자가 가리키는 곳이 파일의 처음부터 몇바이트 떨어진 곳인지 알려줍니다.

<br>

```c
#include <stdio.h>
#pragma warning(disable:4996)

void main()
{
	long pos;

	FILE* fp = fopen("sample.txt", "wt");
	fputs("1234#", fp);
	fclose(fp);

	fp = fopen("sample.txt", "rt");
	
	for (int i = 0; i < 4; ++i)
	{
		// 파일로부터 한 글자씩 읽어 화면에 출력
		putchar(fgetc(fp));
		// 현재 파일 위치 지시자 정보를 pos에 저장
		pos = ftell(fp);

		fseek(fp, -1, SEEK_END);
		putchar(fgetc(fp));

		/* 저장해 놓은 정보를 참조하여
		파일 위치자를 이전 위치로 되돌림 */
		fseek(fp, pos, SEEK_SET);
	}

	fclose(fp);
}
```

<br><br>