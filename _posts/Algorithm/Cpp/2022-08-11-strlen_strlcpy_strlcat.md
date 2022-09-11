---
title:  "[C++] 문자열 함수 (Strlen, strlcpy, strcat, strcmp)"
excerpt: Strlen, strlcpy, strcat, strcmp

categories:
  - Cpp
tags:
  - [Programming, c++, Strlen, strlcpy, strcat, strcmp]

toc: true
toc_sticky: true
 
date: 2022-08-11
last_modified_at: 2022-08-11
---

## 각각 개념 및 코드
---
<br>

### Strlen
---<br>
* 문자열의 길이를 구하는 함수

### 코드 및 실행 결과
---<br>

``` C++
#include <stdio.h>

int Strlen(char* str);

int main()
{
	char text[100];

	printf("Input Text data : ");

	// when you get char or char[] type through scanf_s, you have to write 
	// size of input data like this
	scanf_s("%s", text, sizeof(text));

	printf("Output strlen result : %d \n", Strlen(text));
}

int Strlen(char* str)
{
	int count = 0;
	// before NULL data, count++
	while (str[count] != '\0') {
		count++;
	}
	return count;
} 
```

### strlcpy
---<br>
*  문자열을 복사하는 함수

### 코드 및 실행 결과
---<br>

```  C++
#include <stdio.h>

char* Strcpy(char text1[], char text2[]);

int main()
{
	char cpy_text[100];
	char text_01[100];

	printf("Input Text data : ");

	// when you get char or char[] type through scanf_s, you have to write 
	// size of input data like this
	scanf_s("%s", text_01, sizeof(text_01));
	printf("Output strcpy result : %s \n", Strcpy(text_01, cpy_text));
}

/// <summary>
/// Strcpy Function
/// </summary>
/// <param name="text1"> Original Data </param>
/// <param name="text2"> Array in which copied data will be placed </param>
/// <returns></returns>
char* Strcpy(char text1[], char text2[])
{
	int count_01 = 0;

	while (text1[count_01] != '\0') {
		text2[count_01] = text1[count_01];
		count_01++;
	}
	text2[count_01] = '\0';

	return text2;
}
```

### strcat
---<br>
* 두 문자열을 붙이는 함수

### 코드 및 실행 결과
---<br>

``` C++
#include <stdio.h>

char* Strcat(char text1[], char text2[]);

int main()
{
	char text_01[100];
	char text_02[100];

	printf("Input Text data : ");

	// when you get char or char[] type through scanf_s, you have to write 
	// size of input data like this
	scanf_s("%s", text_01, sizeof(text_01));
	scanf_s("%s", text_02, sizeof(text_02));

	printf("Output strcat result : %s \n", Strcat(text_01, text_02));
}

char* Strcat(char text1[], char text2[])
{
	int count_01 = 0, count_02 = 0;
	while (text1[count_01] != '\0') {
		count_01++;
	}
	while (text2[count_02] != '\0') {
		text1[count_01]= text2[count_02];
		count_01++;
		count_02++;
	}
	text1[count_01] = '\0';

	return text1;
}
```


### strcmp
---<br>
* 두 문자열을 비교하는 함수

### 코드 및 실행 결과
---<br>

``` C++
#include <stdio.h>

char* Strcmp(char text1[], char text2[]);

int main()
{
	char text_01[100];
	char text_02[100] = "star";

	printf("Input Text data_1 : ");

	// when you get char or char[] type through scanf_s, you have to write 
	// size of input data like this
	scanf_s("%s", text_01, sizeof(text_01));

	printf("Output strcpy result : %s \n", Strcmp(text_01, text_02));
}

char* Strcmp(char text1[], char text2[])
{
	char* result_text = new char;
	int text_count = 0;
	while (text1[text_count] != '\0' || text2[text_count] != '\0')
	{
		if (text1[text_count] < text2[text_count] || text1[text_count] > text2[text_count]) {
			return "false";
		} else {
			text_count++;
		}
		
	}
	return "true";
}
```

<br>

[Top](#){: .btn .btn--primary }{: .align-right}