# C언어 2022 기말 실습 — Full Notes

> Notion 원문에서 개인 식별 정보만 제거한 공개본입니다. 실습 코드와 작성 당시의 설명은 학습 기록으로 유지했습니다.

### 1091 - 문자열 비교(대소문자 반전)
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int cmp(char src[][100])
{
    int cnt = 0;
    int cnt2 = 0;
    int cnt1 = 0;
    int a = 'A' - 'a';

    while (src[0][cnt] != NULL) {
        cnt++;
    }
    while (src[1][cnt2] != NULL) {
        cnt2++;
    }
    //printf("%d", cnt);

    if (cnt == cnt2) {
        for (int i = 0; i < cnt; i++) {
            if (src[0][i] >= 'a' && src[0][i] <= 'z') {
                src[0][i] = src[0][i] + a;
            }
            else if (src[0][i] >= 'A' && src[0][i] <= 'Z') {
                src[0][i] = src[0][i] - a;
            }
        }
    }

    for (int i = 0; i < cnt; i++) {
        if (src[0][i] == src[1][i]) cnt1++;
        else break;
    }

    if (cnt1 == cnt)return 1;
    else return -1;
}

int main(void)
{
    char arr[2][100];

    scanf("%s", arr[0]);
    scanf("%s", arr[1]);

    printf("%d", cmp(arr)); // 1 또는 -1이 리턴되어 출력 되는 형태

    return 0;
}
```
코드 설명 : src[0][100]과 src[1][100]의 길이를 구한 다음 같을 때만 실행 되며 둘 중 하나의 문자열만 대문자는 소문자로 소문자는 대문자로 바꾸어서 비교할 문자열과 for문을 사용하여 비교 cnt1을 쓰는 이유는 만약 같다면 cnt1++ 해주어서 cnt1이 원래 cnt와 같다면 모든 배열이 다 같은 것을 의미함으로 cnt1==cnt라면 1을 출력함.
### 1092 - 문자열 비교(대소문자 구분X)
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int cmp(char src[][100])
{
    int cnt = 0;
    int cnt2 = 0;
    int cnt1 = 0;
    int a = 'A' - 'a';

    while (src[0][cnt] != NULL) {
        cnt++;
    }
    while (src[1][cnt2] != NULL) {
        cnt2++;
    }
    //printf("%d", cnt);

    if (cnt == cnt2) {
        for (int i = 0; i < cnt; i++) {
            if (src[0][i] >= 'a' && src[0][i] <= 'z') {
                src[0][i] = src[0][i] + a;
            }
        }
        for (int i = 0; i < cnt; i++) {
            if (src[1][i] >= 'a' && src[1][i] <= 'z') {
                src[1][i] = src[1][i] + a;
            }
        }
    }

    for (int i = 0; i < cnt; i++) {
        if (src[0][i] == src[1][i]) cnt1++;
        else break;
    }

    if (cnt1 == cnt)return 1;
    else return -1;
}

int main(void)
{
    char arr[2][100];

    scanf("%s", arr[0]);
    scanf("%s", arr[1]);

    printf("%d", cmp(arr)); // 1 또는 -1이 리턴되어 출력 되는 형태

    return 0;
}
```
코드 설명 : 대소문자 구분이 없기 때문에 src[0][100]과 src[1][100]을 모두 대문자로 바꾸어 주고 그 후에 같은지를 비교하였다. 그 외에는 1091과 같은 내용의 코드.
### 1093 - 2차원 배열 동적할당
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

char** ese(char** _p)
{
    _p = (int**)malloc(sizeof(int*) * 3);
    for (int i = 0; i < 3; i++) {
        _p[i] = (int*)malloc(sizeof(int) * 30);
    }

    for (int i = 0; i < 3; i++) {
        scanf("%s", _p[i]);
    }
    return _p;

}

int main(void)
{
    char** p = NULL;

    p = ese(p);

    printf("%s\n%s\n%s", *p, *(p + 1), *(p + 2));

    for (int i = 0; i < 3; i++) free(p[i]);
    free(p);

    return 0;
}
```
코드 설명 : 2중 포인터는 한 번 가면 포인터가 있고 한 번 더 가면 int가 있다는 내용으로, 함수에서 p를 이중 포인터로 받은 이유는 \*\*p에서 한 번 가면 \*p로 2차원 배열에서는 만약 p[a][b]가 있다면 a의 자리를 지목한다 그 후에 한 번 더 들어가면 p[a]에서의 [b]까지 들어가게 되는 것이다.  여기서 원하는 배열은 3x30으로 \*_p의 개수를 3개로 만들고 각각 for문을 돌려 30개씩 받을 수 있게 짠 코드이다.
### 1095 - 문자열 안에 특정 문자 개수 카운트
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int  countKey(char* str, char key)
{
    int cnt = 0;
    while (str[cnt] != NULL) {
        cnt++;
    }

    int cnt1 = 0;
    for (int i = 0; i < cnt; i++) {
        if (str[i] == key) cnt1++;
    }
    return cnt1;
}

int main(void)
{
    char str[100];
    char key;

    scanf("%c", &key);
    scanf("%s", str);

    printf("%d", countKey(str, key));

}
```
코드 설명 : 첫 번째로 str의 길이를 구하고 for문을 cnt의 개수 만큼 돌려서 그 안에서 key와 같은 단어가 있다면 cnt1을 사용하여 개수를 세고 그 값을 retrun하도록 코드 작성
### 1096 - 문자열에 문자열 포함여부
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int  isKeyIncluded(char* str, char* key)
{
    int cnt = 0, cnt1 = 0;
    while (str[cnt] != NULL)cnt++;
    while (key[cnt1] != NULL)cnt1++;

    for (int i = 0; i < cnt; i++) {
        if (str[i] == key[0]) {
            int cnt2 = 0;
            for (int j = 0; j < cnt1; j++) {
                if (str[i + j] == key[j]) cnt2++;
                else break;
            }
            if (cnt2 == cnt1)return 1;

        }
    }

    return 0;
}


int main(void)
{
    char str[100];
    char key[10];

    scanf("%s", str);
    scanf("%s", key);

    printf("%d", isKeyIncluded(str, key));

}
```
코드 설명 : str과 key의 길이를 구해주고 for문을 str의 길이 만큼 돌린다. for문 안에서 만약 str[i]가 key의 첫번째 값과 같다면 for문이 실행되는데 key의 길이만큼 실행되고 cnt2를 만들어 주어 같을 때는 cnt2++ 를 해주고 같지 않다면 break로 for문을 나오게 하였다. 그러고 나서 만약 cnt2와cnt1(key의 길이)가 같다면 return 1(포함 되어있다)를 출력하고 없다면 reture 0(포함되어 있지 않다)를 출력하도록 하였다. cnt2를 if 다음과 for문 사이에 만든 이유는 두번째 for문을 돌고 나면 0으로 다시 초기화를 해주어야 하기 때문이다 만약 하지 않는다면 cnt2의 길이는 계속 길어지게 된다.
### 1097 - 2진수 값에 따라 문자열로 표현
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>


void makeDot(unsigned int data, char* _binary)
{
    unsigned int a = 1<<31;
    //printf("%d", a);
    for (int i = 0; i <32; i++) {
        ((data & a) == 0) ? (_binary[i] = '-') : (_binary[i] = '*');
        a = a >> 1;
    }
}

int main(void)
{
    unsigned int data;
    char binary[33];
    scanf("%u", &data);

    makeDot(data, binary);
    binary[32] = NULL;

    printf("%s", binary);
    return 0;
}
```
 코드 설명 :  unsigned int를 한 이유는 31로 보내면 int의 범위를 넘어가기 때문이다 int의 범위는 128까지인데 128을 2진수로 나타내면 1000,0000인데 31로 보내면 1000,0000,0000,0000,0000,0000,0000,0000 이기 때문에 범위를 늘리기 위해서는 어차피 우리는 양수만 사용하기 때문에 음수의 범위를 없애고 양수의 범위를 넓히기 위해서 이렇게 사용하였다. 그 후에 for문을 32번 돌려서 data와 a의 &연산(비트연산)을 하고 만약 0이라면 _binary[i]에는 -이 저장되고 1이면 \*가 저장하며 저장한 뒤에는 a를 원래 a보다 1 한 칸 뒤로 보내면서 반복하는 형식으로 코드를 작성하였다.
### 1098 - 문자열 안에 특정 문자 포함 여부
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int  countKey(char* str, char key)
{
    int cnt = 0;
    while (str[cnt] != NULL) {
        cnt++;
    }

    int cnt1 = 0;
    for (int i = 0; i < cnt; i++) {
        if (str[i] == key) cnt1++;
    }

    if (cnt1 > 0)return 1;
    else return 0;
}

int main(void)
{
    char str[100];
    char key;

    scanf("%c", &key);
    scanf("%s", str);

    printf("%d", countKey(str, key));

}
```
코드 설명 : str의 길이를 구한 뒤 길이 만큼 for문을 돌려서 str과 key가 같으면 cnt1++ 해준다. 그 후 만약 cnt1이 0보다 크다면 str안에 key가 포함되었기 때문에 return 1을 해주고 만약 0이거나 0이라면 아무것도 포함되지 않은 것이기 때문에 return 0을 해준다.
### 1099 - 2진수 값에 따라 문자열로 표현, binary 1개의 개수
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>


int makeDot(unsigned int data, char* _binary)
{
    unsigned int a = 1 << 31;
    //printf("%d", a);
    for (int i = 0; i < 32; i++) {
        ((data & a) == 0) ? (_binary[i] = '!') : (_binary[i] = '@');
        a = a >> 1;
    }
    int cnt = 0;
    for (int i = 0; i < 32; i++) {
        if (_binary[i] == '@')cnt++;
    }
    return cnt;
}

int main(void)
{
    unsigned int data;
    char binary[33];
    scanf("%u", &data);

    printf("%d\n", makeDot(data, binary));
    binary[32] = NULL;

    printf("%s", binary);
    return 0;
}
```
코드 설명 : 문제 1097과 거의 비슷하지만 binary 1의 개수를 세는 것만 추가되었다. 1의 개수를 세는 방법은 for문을 32번 돌리면서  _binary 문자열에  @가 있다면 cnt++ 하는 방식으로 해서 1의 개수를 구하였다.
### 1100 - 문자열에 문자열 포함
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int  isKeyIncluded(char* key, char* str)
{
    int cnt = 0, cnt1 = 0;
    while (str[cnt] != NULL)cnt++;
    while (key[cnt1] != NULL)cnt1++;

    for (int i = 0; i < cnt; i++) {
        if (str[i] == key[0]) {
            int cnt2 = 0;
            for (int j = 0; j < cnt1; j++) {
                if (str[i + j] == key[j])cnt2++;
                else break;
            }
            if (cnt2 == cnt1)return 1;
        }
    }
    return 0;
}

int main(void)
{
    char key[10];
    char str[100];

    scanf("%s", key);
    scanf("%s", str);

    printf("%d", isKeyIncluded(key, str));

}
```
코드 설명 : str과 key의 길이를 구한 뒤 str의 길이 만큼 for문을 돌리는 데, 그때 str[i]의 값과 key의 첫번째 값이 같다면 for문을 key의 길이만큼 돌려서 만약 str[i+J]와 key[j]의 값이 같다면 cnt2++ 해서 만약 cnt2와 cnt1의 길이가 같다면 이것은 key가 srt에 포함된다는 뜻으로 return 1을 해준다. 만약에 같지 않다면 for문을 빠져나오게 되는데 그대로 return 0으로 가게 된다.
### 1101 - 동적할당, 모든 원소의 합
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

int** makeArrayDynamic(int** _p, int _size)
{
    _p = (int**)malloc(sizeof(int*) * _size);
    for (int i = 0; i < _size; i++) {
        _p[i] = (int*)malloc(sizeof(int) * _size);
    }
    return _p;
}
int sumofArray(int** _p, int _size)
{
    int add = 0;
    for (int i = 0; i < _size; i++) {
        for (int j = 0; j < _size; j++) {
            add = add + _p[i][j];
        }
    }
    return add;
}

int main() {

    int** p = NULL;
    int size, sum = 0;

    scanf("%d", &size); // 정사각 배열 사이즈를 입력받음.

    // [size x size] 크기의 배열 동적할당
    p = makeArrayDynamic(p, size);  // <- 1. 이 함수 구현


    // 배열에 원소 값을 순차적으로 입력
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            scanf("%d", &p[i][j]);
        }
    }

    // 배열 내에 있는 모든 원소의 합
    sum = sumofArray(p, size);   // <- 2. 이 함수 구현

    printf("%d", sum); // 합 출력

    // 동적할당 free
    for (int i = 0; i < size; i++) free(p[i]);
    free(p);

    return 0;
}
```
코드 설명 : makeArrayDynamic 함수에서는 이중 포인터를 사용하여 2차원 배열로 _p에게 공간을 할당하였다. 그 후 sumofArray에서는 이중 for문을 사용하여 add라는 정수에다가 계속 더해준 후 return add값을 하여 배열의 모든 정수의 합을 표현하였다.
### 1102 - 동적할당, 짝수의 개수
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

int** makeArrayDynamic(int** _p, int _size)
{
    _p = (int**)malloc(sizeof(int*) * _size);
    for (int i = 0; i < _size; i++) {
        _p[i] = (int*)malloc(sizeof(int) * _size);
    }
    return _p;
}
int countEven(int** _p, int _size)
{
    int cnt = 0;
    for (int i = 0; i < _size; i++) {
        for (int j = 0; j < _size; j++) {
            if (_p[i][j] % 2 == 0)cnt++;
        }
    }
    return cnt;
}

int main() {

    int** p = NULL;
    int size, cnt = 0;

    scanf("%d", &size); // 정사각 배열 사이즈를 입력받음.

    // [size x size] 크기의 배열 동적할당
    p = makeArrayDynamic(p, size); // <- 1. 이 함수 구현


    // 배열에 원소 값을 순차적으로 입력
    for (int i = 0; i < size; i++) {
        for (int j = 0; j < size; j++) {
            scanf("%d", &p[i][j]);
        }
    }

    // 배열 내에 있는 짝수인 원소의 개수
    cnt = countEven(p, size); // <- 2. 이 함수 구현

    printf("%d", cnt); // 합 출력

    // 동적할당 free
    for (int i = 0; i < size; i++) free(p[i]);
    free(p);

    return 0;
}
```
코드 설명 : makeArrayDynamic 함수에서는 _p를 이중 포인터를 사용하여서 2차원 배열로 공간을 할당하였다.
countEven함수에서는 이중 for문을 사용하여 _p[i][j]에서 2를 나눴을 때 나머지가 0이면 cnt++ 하여 return cnt를 하면 짝수의 개수가 나오게 된다.
### 1103 - 2차원 배열 정수배
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>


// scalarMultiple 함수 구현 ===================
void scalarMultiple(int add[3][4], int n)
{
    int add1[3][4]={0,};
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            add1[i][j] = add[i][j];
        }
    }

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            add[i][j] = add1[i][j] * n ;
        }
    }
}
// ===================================


int main() {

    int arr[3][4];
    int n = 0;
    scanf("%d", &n);

    // 입력
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            scanf("%d", &arr[i][j]);
        }
    }

    // scalarMultiple 함수 호출 부분 (여기에 작성)==========
    scalarMultiple(arr, n);
    // =====================================

    // 출력
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```
코드 설명 : scalarMultiple 함수에서 for문을 사용하여 add에 있는 정수를 add1으로 옮기고 다시 for문을 사용해서 add에다가 add1과 n을 곱한 값을 넣어주었다.
### 1104 - 2차원 배열 n제곱
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

// makePow 함수 구현 ====================
void makePow(int arr[3][4], int n)
{
    int arr1[3][4] = { 0, };
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            arr1[i][j] = arr[i][j];
        }
    }
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            if (n > 0) {
                for (int k = 0; k < n-1; k++) {
                    arr[i][j] = arr1[i][j] * arr[i][j];
                }
            }
            else {
                arr[i][j] = 1;
            }
        }
    }
}
// ===================================

int main() {

    int arr[3][4];
    int n = 0;
    scanf("%d", &n);

    // 입력
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            scanf("%d", &arr[i][j]);
        }
    }

    // makePow 함수 호출 부분 (여기에 작성)==========
    makePow(arr, n);
    // ==================================

    // 출력
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 4; j++) {
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```
코드 설명 : 맨처음에 arr1이라는 배열을 만들어서 arr 배열을 복사해준다. 그 이유는 만약 n이 3이라서 arr =arr\*arr을 한다면 for문이 두번째로 돌 때는 arr=arr\^2\*arr\^2이 되기때문에 4제곱의 값이 나온다. 그것을 방지하기 위해서 이고 이중 for문 안에서 만약 n이 0이라면 모든 수의 0승은 1이기 때문에 arr안 정수를 모두 1로 바꾸어 주고 만약 0보다 크다면 for문을 n만큼 더 돌려서 arr=arr\*arr1을 해주면 된다.
### 1105 - 일치하는 문자 개수
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int cmp(char str[2][100])
{
    int cnt = 0, cnt1 = 0;
    while (str[0][cnt] != NULL) cnt++;
    while (str[1][cnt1] != NULL)cnt1++;
    int cnt2 = 0;
    if (cnt >= cnt1) {
        for (int i = 0; i < cnt1; i++) {
            if (str[0][i] == str[1][i]) cnt2++;
        }
    }
    else if (cnt < cnt1) {
        for (int i = 0; i < cnt; i++) {
            if (str[0][i] == str[1][i])cnt2++;
        }
    }
    return cnt2;
}

int main() {

    char str[2][100];
    int cnt = 0; // 같은자리 같은문자 개수

    // 입력
    scanf("%s", str[0]);
    scanf("%s", str[1]);

    // cmp 함수 호출 ====================
   cnt = cmp(str);
    // =============================

    //출력
    printf("%d", cnt);

    return 0;
}
```
코드 설명 : str[0]과 str[1]의 문자열 길이를 구한 뒤 만약 str0보다 str1이 길면 str0까지 for문을 돌리고 반대로 str1 보다 str0이 길면 str1까지 for문을 돌려서 같은 자리에 같은 문자가 있는지 확인해본다. 이렇게 하는 이유는 만약 큰 값으로 for문을 돌리게 된다면 혹시나 쓰레기 값이 같은 자리에 똑같이 있을 확률이 있기 때문이다. for 문을 돌린 후에 if문으로 str[0][i] == str[1][i]라면 cnt2++ 해주어 같은 자리에 같은 문자의 개수를 세주고 return cnt2로 main에 값을 보내준다.
### 1106 -  문자열의 행을 바꾸기
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

void swap(char str[2][100])
{
    int cnt = 0;
    char str1[2][100];
    while (str[1][cnt] != NULL)cnt++;
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < cnt; j++) {
            str1[i][j] = str[i][j];
        }
    }
    for (int i = 0; i < cnt; i++) {
        str[0][i] = str1[1][i];
        str[1][i] = str1[0][i];
    }
}

int main() {

    char str[2][100];

    // 입력
    scanf("%s", str[0]);
    scanf("%s", str[1]);

    // swap 함수 호출 ====================
    swap(str);
    // =============================

    //출력
    printf("%s\n%s", str[0], str[1]);

    return 0;
}
```
코드 설명 : 문제에서 str[0]과 str[1]의 문자열 길이가 같다고 하였으니 둘 중 하나의 길이를 구한 뒤, 새로운 문자열 str1를 만들어서 str을 str1에 복사해준다. 그러면 str1의 [1][i]을 str[0][i]에 바꾸어 주고 str1[0][i]을 str[0][i]에 바꾸어 주면 문자열 두개가 바뀌게 된다.
### 1107 - 동적할당 전치
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

int main() {

    int** p = NULL;
    int** q = NULL;

    int a, b; // 순서대로 행, 열
    scanf("%d %d", &a, &b);

    // 코드 작성 ==============================
    p = (int**)malloc(sizeof(int*) * a);
    for (int i = 0; i < a; i++) {
        p[i] = (int*)malloc(sizeof(int) * b);
    }
    q = (int**)malloc(sizeof(int*) * b);
    for (int i = 0; i < b; i++) {
        q[i] = (int*)malloc(sizeof(int) * a);//q는 p와 반대 배열이다!! a랑b자리 바꿔
    }
    for (int i = 0; i < a; i++) {
        for (int j = 0; j < b; j++) {
            scanf("%d",&p[i][j]); //p는 int형이야 제발 &넣자!!
        }
    }

    for (int i = 0; i < b; i++) {
        for (int j = 0; j < a; j++) {
            q[i][j] = p[j][i];
        }
    }
    // ====================================

    // 출력
    for (int i = 0; i < b; i++) {
        for (int j = 0; j < a; j++) {
            printf("%d ", q[i][j]);
        }
        printf("\n");
    }

    // 동적할당 free
    for (int i = 0; i < a; i++) free(p[i]);
    free(p);
    for (int i = 0; i < b; i++) free(q[i]);
    free(q);

    return 0;
}
```
코드 설명 : p와 q의 동적할당으로 공간을 할당하지만 여기서 주의해야 할 점은 만약 p가 2x3배열이면 q는 3x2 배열이기 때문에 똑같이 할당해서는 안 되고 정반대로 할당해야 한다. 그 후에 for문으로 p의 값을 받는데 대신 p는 int형 배열이니까 제발 & 붙이자! 그 후에 for문 돌려서 반대로 i는 b까지 j는 a까지로 두고 q[i][j]=p[i][j]로 할당해주면 끝 왜 저렇게 하는지는 사진을 통해 이해 
### 1108 - 동적할당 reshape
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

int main() {

    int p[100];
    int** q = NULL;

    int size; // 배열 p의 사이즈
    int n; // 몇 행으로 만들 것인가

    scanf("%d %d", &size, &n);

    // 여기에 코드 작성 =======================================
    for (int i = 0; i < size; i++) {
        scanf("%d", &p[i]);
    }
    q = (int**)malloc(sizeof(int*) * n);
    for (int i = 0; i < n; i++) {
        q[i] = (int*)malloc(sizeof(int) * (size / n));
    }
    if (size % n == 0) {
        int a = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < size / n;j++) {
                q[i][j] = p[a++];
            }
        }
    }
    else {
        printf("ERROR");
        return 0;
    }
    // =================================================

    // 출력
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < size / n; j++) {
            printf("%d ", q[i][j]);
        }
        printf("\n");
    }

    // 동적할당 free
    for (int i = 0; i < n; i++) free(q[i]);
    free(q);

    return 0;
}
```
코드 설명 :  일단 for문 사용하여 size만큼 p에다가 정수를 입력 받고, q를 동적할당 해주는데 n이 행의 개수로 그러면 열의 개수는 size/n이 된다. 동적할당을 n개로 각각 size/n으로 받은 후 만약 size%n이 0이라면 맞아 떨어지니까 for문을 사용해서 q한테 p의 값을 주어야 하는데 p는 1차원 배열이고 만약 size가 16이라면 0부터 15까지 커지면 되니까 q[i][j]와는 다른 변수인 a를 지정하여 a++ 해준다. 그러면 완성\~
### 1109 - 포인터 배열 동적할당과  함수
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

int makeArrayandInput(char* str[6])
{
    for (int i = 0; i < 6; i++) {
        str[i] = (int*)malloc(sizeof(int) * 100);
    }

    for (int i = 0; i < 6; i++) {
        scanf("%s", str[i]);
    }

    return str;
}

int main() {

    char* str[6];

    makeArrayandInput(str);

    // 출력
    for (int j = 0; j < 6; j++)
    {
        printf("%s\n", str[j]);
    }

    // 동적할당 free
    for (int i = 0; i < 6; i++) free(str[i]);

    return 0;
}
```
코드 설명 :  main함수에서 \*str[6]은 이미 \*\*str에서 한번 가르킨 것이다. 그래서 makeArrayandInput 함수에서 \*str에서 100개의 공간을 할당하기 위해 for문으로 할당하였고 그 후에 6개의 문자열을 입력받았다.
### 1110 - 2차원 배열과 함수
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

void getInputValue(char str[6][100])
{
    for (int i = 0; i < 6; i++) {
        scanf("%s", str[i]);
    }
}
void printValue(char str[6][100])
{
    for (int i = 0; i < 6; i++) {
        printf("%s\n", str[i]);
    }
}

int main() {

    char str[6][100];

    getInputValue(str);

    printValue(str);

    return 0;
}
```
코드 설명 : for문 돌려서 6개의 문자열을 받고 for문을 돌려서 6개의 문자열을 내보낸다.
### 1111 - 문자열 안에 문자열 포함(대소문자 구분X)
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int isKeyIncluded(char str[100], char key[10])
{
    int cnt = 0, cnt1 = 0;
    int a = 'A' - 'a';
    while (str[cnt])cnt++;
    while (key[cnt1])cnt1++;

    for (int i = 0; i < cnt; i++) {
        if (str[i] >= 'a' && str[i] <= 'z') {
            str[i] = str[i] + a;
        }
    }
   // printf("%s", str);
    
    for (int i = 0; i < cnt1; i++) {
        if (key[i] >= 'a' && key[i] <= 'z') {
            key[i] = key[i] + a;
        }
    }
   // printf("%s", key);

    for (int i = 0; i < cnt; i++) {
        if (str[i] == key[0]) {
            int cnt2 = 0;
            for (int j = 0; j < cnt1; j++) {
                if (str[i + j] == key[j])cnt2++;
            }
            if (cnt2 == cnt1) return 1;
        }
    }
    return 0;
}

int main(void)
{
    char str[100];
    char key[10];

    scanf("%s", str);
    scanf("%s", key);

    printf("%d", isKeyIncluded(str, key));
    return 0;

}
```
코드 설명 : str과 key의 길이를 구한 뒤 for문을 통해 str과 key에서 만약 소문자가 있다면 대문자로 변환해준 뒤, for문을 str의 길이만큼 돌리면서 만약 str[i]와 key[0]이 같다면 for문을  key의 길이만큼 돌리고 cnt2로 같은 개수를 센다. 만약 cnt2와 key의 길이가 같으면 str에 key가 포함되었으니 return 1을 해주고 만약 return 1을 못하고 for문을 빠져나왔다면 str안에는 key가 없으므로 return 0을 하였다.
### 1112 - 구조체 멤버 값 비교, 조작하기
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
struct student {
    char name[10];
    int age;
    int height;
}s1,s2;

int main()
{
    scanf("%s %d %d", s1.name, &s1.age, &s1.height);
    scanf("%s %d %d", s2.name, &s2.age, &s2.height);

    if (s1.age == s2.age) {
        char a[10] = "SAME";
        for (int i = 0; i < 10; i++) {
            s1.name[i] = a[i];
            s2.name[i] = a[i];
        }
    }
    else if (s1.age > s2.age) {
        for (int i = 0; i < 10; i++) {
            s2.name[i] = s1.name[i];
        }
    }
    else{
        for (int i = 0; i < 10; i++) {
            s1.name[i] = s2.name[i];
        }
    }

    printf("%s %d %d\n", s1.name, s1.age, s1.height);
    printf("%s %d %d", s2.name, s2.age, s2.height);
}
```
코드 설명 : 구조체를 할당하고 스캔 받은 뒤 만약 s1.age와 s2.age가 같다면 char a[10]=”SAME”으로 두고 둘 다 for문으로 바꾼다. 만약 s1\>s2라면 s1의 이름을 s2에 할당하였고, 반대로 s2\>s1이라면 s2의 이름을 s1에 할당하였다. 주의해야할 점은 s1.age와 s2.age, s1.height, s2.height는 정수 값이기 때문에 scanf 받을 때 &써주는 것 잊지 말기!
### 1113 - 대문자만 복사하는 문자열
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

void esestrcpy(char result[100], char arr[100])
{
    int cnt = 0;
    while (arr[cnt] != NULL)cnt++;
    int a = 0;
    for (int i = 0; i < cnt; i++) {
        if (arr[i] >= 'A' && arr[i] <= 'Z') {
            result[a++] = arr[i];
        }
    }
    if (a > 0)result[a] = NULL;
    else result[0] = NULL;
}

int main(void)
{
    char arr[100];
    char result[100];

    scanf("%s", arr);

    esestrcpy(result, arr);

    printf("%s", result);
    return 0;
}
```
코드 설명 :일단 arr의 길이를 세주고 for문에서 arr의 길이만큼 돌린 다음에 만약 arr[i]가 대문자라면 result에 넣어주는 코드이다. a++로 따로 쓴 이유는 i는 항상 증가하지만 result는 대문자를 만났을 때만  증가하기 때문이다. 만약 대문자가 없다면 바로 result가 null이 되어야 해서 만약 a가 0보다 크면 result[a]=NULL로 하여 마지막부분에 0을 넣어주고 0보다 작다면 result의 첫번째 값에 0을 넣어준다. 여기서 주의할 점은 함수한테 부여할 때 순서 헷갈리지 말기! 또 마지막에는 항상 쓰레기 값이 들어있기 때문에 마지막 부분은 null로 채워주기
### 1114 - 문자열 조작하기(연속된 문자 개수로)
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

void esefix(char data[100], char result[100])
{
    int cnt = 0;
    while (data[cnt] != NULL)cnt++;
    int a = 0;
    for (int i = 0; i < cnt; i++) {
        int cnt2 = 0;
        for (int j = 0; j < cnt; j++) {
            if (data[i] == data[i + j])cnt2++;
            else break;
        }
        if (cnt2 == 0)cnt2 = 1;
        result[a++] = cnt2+'0';
        result[a++] = data[i];
        i = i + cnt2 - 1;
    }
    result[a] = NULL;
}


int main() {

    char data[100]; // 입력 받은 값 저장하는 배열
    char result[200]; // 변형된 결과 저장하는 배열

    scanf("%s", data);

    esefix(data, result);

    printf("%s", result); // 변형된 결과 배열 출력

    return 0;
}

```
코드 설명 : data의 길이를 구한 뒤 for문을 data의 길이만큼 돌리고 이중 for문으로 한 번 더 돌려서 data[i]와 data[i+j]가 같은 개수를 구한다. 만약 cnt2가 0이면 단어 개수는 1개이기 때문에cnt2=1로 해주고 result에다가 a++를 넣어주는 이유는 i와 j는 이중적으로 돌아가지만 result는 계속 증가하면서 값을 넣어주기 때문이며 가장 핵심포인트는 cnt2+’0’부분이다. ‘0’은 0의 아스키코드로 cnt2는 정수이지만 우리는 char의 문자열에 넣어주는 것이기 때문에 정수를 아스키코드 값으로 바꿔줘야 한다. i=i+cnt2-1의 이유는 for문에서 i++를 for문 들어가기 전에 한 번 더 해주기 때문이다. 마지막에 result에 null값을 넣어주는 것도 주의해야한다. 만약 안 넣으면 쓰레기 값이 나온다.
### 1118 - 1차원배열 동적할당 최대 최소값
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
int main()
{
    int n = 0;
    scanf("%d", &n);
    int* p = 0;
    p = (int*)malloc(sizeof(int) * n);

    for (int i = 0; i < n; i++) {
        scanf("%d", &p[i]);
    }

    int min = p[0]; 
    int max = p[0];

    for (int i = 0; i < n; i++) {
        if (max < p[i])max = p[i];
    }

    for (int i = 0; i < n; i++) {
        if (min> p[i])min = p[i];
    }

    printf("%d %d", max, min);
}
```
코드 설명 : p로 n만큼 할당 받고 min과 max 변수를 만들고 p의 맨 처음 값을 넣어준다. 그리고 for문을n만큼 돌리면서 max부분에서는 max보다 p[i]값이 크면 max값을 p[i]의 값으로 교체하도록 하였고 반대로 min은 min보다 p[i]가 작다면 p[i]의 값으로 교체하도록 작성하였다.
### 1119 - 구조체 배열 정렬하기
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
struct a {
    char name[10];
    int s;
}st[10],temp;

int main()
{
    int n = 0;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%s %d", st[i].name, &st[i].s);
    }
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (st[i].s > st[j].s) {
                temp = st[i];
                st[i] = st[j];
                st[j] = temp;
            }
        }
    }

    for (int i = 0; i < n; i++) {
        printf("%s %d\n", st[i].name, st[i].s);
    }

}
```
코드 설명 : 구조체를 만들 때, temp를 만들어준 이유는 struct(구조체)는 복사가 가능하기 때문이다. scanf을 받고 이중 for문을 돌려서 만약 n=3이고, st[i].s일때 st[0].s과 st[1].s, st[2].s를 돌려서 큰 것을 찾고 그럴때마다 temp로 큰 것을 저장하고 그 값을 st[j]에다가 넣어주는 것이다.
### 1126  - 16진수처럼 입력된 문자열을 10진수 형태에서의 0의 개수 구하기
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int countZero(char str[9])
{
    int sum = 0;m
    int cnt = 0;
    while (str[cnt] != NULL)cnt++;
    for (int i = cnt-1; i>=0; i--) {
        int a = 0;
        if (str[i] >= '0' && str[i] <= '9')a = str[i] - '0';
        else if (str[i] >= 'A' && str[i] <= 'Z')a = str[i] - 'A' + 10;
        else if (str[i] >= 'a' && str[i] <= 'z')a = str[i] - 'a' + 10;
        //printf("%d\n", a);
        int b = 1;
        for (int j = 0; j < cnt - i - 1; j++) b = b * 16;
        sum=sum+a*b;
          //printf("%d\n", sum);
    }
  

    int cnt2 = 0;
    while (sum > 0) {
        if (sum % 10 == 0)cnt2++;
        sum = sum / 10;
    }
    
    return cnt2;
}
int main() {

    char str[9];
    scanf("%s", str);

    printf("%d", countZero(str));

    return 0;
}
```
코드 설명 : 일단 str의 길이를 구하고 16진수의 계산법이 만약 123이라면 (16\^0\*3)+(16\^1\*2)+(16\^2\*1)이렇게 계산하는 것이기 때문에 거꾸로 시작해야한다. (3부터 시작) 일단 char로 받아서 문자열 안에 들어간 숫자나 문자는 진짜 16진수가 아닌 아스키코드 이므로 아스키코드를 정수로 바꾼 값을 a에 넣고 변수 b는 제곱의 합을 나타내 주는 것인데, 모든 수의 0승은 1라는 것이 포인트 이다. for문을 돌려서 j의 값이 cnt-i-1인 이유는 만약 cnt값이 3이라서 i의 값이 2라면 cnt-2-1은 0이기 때문이다. j가 0일때 j\<0이면 for문은 돌아가지 않고 그러면 sum=sum+a\*b로 바로 넘어가서 sum = a가 된다. 내가 몰랐던 것(b=b\*16) 그 후에 수를 다 구한 뒤에 10진수에서 0의 개수를 구하려면 일단 sum을 10으로 나눠준다 만약 sum이 10이라면 10/10은 몫이 1이고 나머지는 0으로 cnt2++하여 cnt2=1이고 sum=sum/10이므로 0이기에 while문을 나가게 된다. 만약
1002라면 1002/10하면 몫은 100이고 나머지는 0이 아니므로 cnt2++가 되지 않는다. sum=sum/10이기에 sum은 100이 되고 한번 더 돌리면 100/10은 몫은 10 나머지는 0 이면서 cnt2++가 된다. sum=10이 되고 한번 더 10으로 나누면 몫은 1 나머지는 0이 되며 cnt2++가 되고, sum=1이니까 10으로 나누면 몫도 0이고 나머지도 1이기에 cnt2는 ++되지 않는 채로 while문을 빠져나가게 된다. 그러면 cnt2=2가 된다. 이렇게 0의 개수를 구하고 return 해주면 된다.
### 1130 - 한글 문자열에 공백 추가하기
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
void AddBlank(char input[100], char output[300])
{
    int cnt = 0;
    while (input[cnt] != NULL)cnt++;

    int a = 0;
    for (int i = 0; i < 300; i++) {
        output[i] = input[a++];
        if (i % 4 == 3) {
            output[i] = ' ';
            a--;
        }
    }
    output[a] = NULL;
}

int main() {

    unsigned char input[100], output[300];

    scanf("%s", input);

    AddBlank(input, output); 

    printf("%s", output);

    return 0;
}
```
코드 설명 : input의 길이를 구하고 for문은 i를 300까지 넣어주는데 그 이유는 input의 길이에다가 3번씩 나올때마다 띄어쓰기를 하기때문에 얼만큼 공간을 차지하는지 모르기 때문이다. output이 2일때까지는 잘 나오다가 i가 3, 7, 11, 15일때는 띄어쓰기를 해야 하는데 이 특징은 모두 4로 나누면 나머지가 3이된다는 점이다. 그래서 if문을 사용하여 i%4가 3이라면 output에 빈칸을 만들지지만 만약 a—를 하지않는다면 aaabbbccc를 넣었을 때, aaa bbc c 이런식으로 나올 것이다. 그래서 a—는 다시 첫번째 b의 자리로 돌아가라는 의미이다. 마지막으로 output[a]에 NULL을 넣어주면서 쓰레기 값이 들어오지 못하게 막는다.

