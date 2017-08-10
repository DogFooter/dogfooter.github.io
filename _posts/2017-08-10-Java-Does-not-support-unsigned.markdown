---
layout: post
title: Java에서 Unsigned를 만났을 때
tag: [Java, Unsigned, unsigned int, 자바]
category: blog
date: 2017-08-10 14:10
headerImage: false
author: dogfooter
comments: true
--- 

Java에서는 기본적으로 unsigned type을 지원하지 않는다. 모든 type이 signed type이다. 이 점은 자바프로젝트에서 간혹 바이너리 파일을 뜯어고치거나 네트워크 관련 작업을 할 때 골치가 아프다. Checksum이라도 구해서 수정해야 하는 일이 발생한다면 머리가 아파진다.

인턴업무 중 font의 subset을 만들며 checksum을 수정해야 할 일이 있었다. 해당 font type의 reference에서는 C를 기준으로 unsigned type을 사용하는 checksum 알고리즘을 제공했다. 이를 계기로 Java로 unsigned를 처음 다뤄보게 되었는데 그 후기를 작성하고자 한다.


## 왜 자바는 unsigned type을 지원하지 않는거야?

가장 큰 의문이었다. C처럼 언어차원에서 지원해주면 쉽게 해결될 문제일 거라 생각했다. 자바를 개발한 고슬링은 unsigned에 대하여 이렇게 언급했다.

>   ... Quiz any C developer about unsigned, and pretty soon you discover that almost no C developers actually understand what goes on with unsigned, what unsigned arithmetic is....  -James Gosling

나도 unsigned type를 정확히 이해하고 있지는 않다. 단순히 signed type에서 부호로 사용하던 MSB의 의미를 지우고 한 비트라도 더 늘려서 사용한다고만 이해했다. 

unsigned를 사용할 때도 딱히 의도하고 사용한 것이 아닌 API에서 사용하는 type이 그렇다면 그렇게 사용한 것이 전부였다. unsigned에 대한 조사를 하고 다음 포스팅 주제로 해도 괜찮을 것 같다.

아무튼 고슬링은 이러한 이유로 unsigned type을 지원하지 않는다고 했다. 지금이야 자바에서 unsigned를 다른 방법으로 지원하기도 한다. 

```java
// Integer같은 wrapper class에서 toUnsignedLong과 같이 지원하기도한다.
// Since Java 1.8
integer1.toUnsignedLong()
```

## 그래도 나는 unsigned를 원한다 
Unsigned type을 그래도 사용해야 할 상황이 생긴다. 위에서 말한 Checksum을 구하는 경우 unsigned로 표현하여 출력해줘야 할 경우가 생긴다. 이럴 경우 어떻게 Unsigned type을 사용해야 하는지 알아보자.

### Unsigned Integer

4바이트의 signed Integer의 표현범위는 $$-2 ^ {31} , 2^{31} -1$$ 이다. Unsigned Integer의 표현범위는 $$0, 2^{32} -1$$ 이다. 

사실 __연산__이라는 측면에서는 signed type과 unsigned type을 구분할 필요는 없다. signed type에서  $$2^{31} -1$$ 을 넘어가는 숫자를 입력한다고 해도 Unsigned type의 $$2^{32} -1$$ 까지 입력이 가능하다. 단순히 출력값으로 표현될 때 표현 범위가 초과하면 해당하는 음수 값을 보여주는 것 뿐이다.

여기서 알 수 있는 점은 단순히 Checksum을 구현할 때는 signed type을 그대로 사용해도 괜찮다. 다만 주의할 점은 byte Array에서 4개씩 뽑아내어 Unsigned Integer을 만들어 그 값을 사용한다면 이야기가 달라진다. 

### byte [] 에서 unsigned integer 뽑아내기

어떤 바이너리 파일에있는 값을 hex로 바꾸어 표현해 보았을때 다음과 같다 가정해보자.

```java
// 편의를 위해 1byte씩 표현하였습니다.
0xAC 0x45 0xBB 0x77 ...
```

Java의 byte type Array에 이 값들을 하나씩 저장하여 프로젝트를 진행했다고 하고, 우리는 다음과 같은 checksum을 구해야한다.

```C
uint32 CalcTableChecksum(uint32 *table, uint32 numberOfBytesInTable)
    {
    uint32 sum = 0;
    uint32 nLongs = (numberOfBytesInTable + 3) / 4;
    while (nLongs-- > 0)
        sum += *table++;
    return sum;
}
// 출처 : https://developer.apple.com/fonts/TrueType-Reference-Manual/RM06/Chap6.html
```

애초에 파일을 1 byte 가 아닌 4 byte 단위로 다시 불러오면 편하겠지만, file의 크기가 매 우크다면 이는 좋지 못한 방법이다. 우리는 byte Array에서 4개씩 꺼내어 uint32 이라는 type에 맞춰주어야 한다. 단순히 생각하면 byte값을 32bit 크기의 type에 넣어 각 자리만큼 shift 하여 더하면 된다.

```java
/**
* binaryArray	: byte []
*					배열의 길이가 4의 배수라고 가정.
* target		: int
*/
for (int i = 0; i < binaryArray.length; i +=4) {
  target = 0;
  for (int j = 0; j < 4; j++) {
    target += ((int) binaryArray[i + j]) << (3 - j) * 8;
  }  
  ...
}
```

그러나 이 변환엔 큰 문제가 있다. 바로 signed type이기 때문에 일어나는 문제이다.

우리가 사용한 source binary file은 다음과 같은 값을 갖고있다.

```java
0xAC 0x45 0xBB 0x77 ...
```

여기서 주의해야 할 점은 몇몇 값들이 byte type의 양의 한계 값인 $$2^{7}-1$$ ```==(0x7F)```을 넘긴다는 것이다.  왜 이점을 주의해야 하냐면 배열에서 값을 가져와 int type으로 변환하는 과정에서 문제가 발생하기 때문이다.

맨 처음 값인 ```0xAC```는 단순히 계산했을 때 172라는 값을 가진다. 이는 $$2^{7}-1$$을 초과하는 값이다. 그래서 byte type에 들어가게 되면 -84라는 값을 의미한다. 이를 int로 type casting을 하게 되면 시스템에선 값을 이렇게 인식하게 된다.

```java
0xFFFFFFAC
```

누군가는 당황스럽고, 또 누군가는 당연하다고 생각한다. 이런 결과의 이유는 integer에서 -84를 넣고 hex 값으로 바꾸게 되면 저 값이 나오기 때문이다. 우리가 필요한 값은 뒤에 한 바이트의 ```0xAC ``` 값 뿐이다. 이 값을 추출하기 위해선 한 가지 비트연산을 거쳐야 한다.

```java
 target += (((int) binaryArray[i + j]) & 0xFF)<< (3 - j) * 8;
```

int type 으로 캐스팅해준 값에 0xFF를 AND 해주었다. 이를 마스킹(masking)이라고 하는데 간단히 말하면 비트 시퀀스에서 원하는 값을 뽑아오는 걸 말한다.  즉 마스킹을 이용하여 뒤의 AC만 살리고 나머지는 0으로 만들어 integer에서 172를 의미하게 만드는 것이다.

```java
    0xFFFFFFAC
AND 0x000000FF
---------------
 =  0x000000AC
```

이를 적용하여 다시 uint32에 맞게 값을 얻을 수 있다.

```java
/**
* binaryArray	: byte []
*					배열의 길이가 4의 배수라고 가정.
* target		: int
*/
for (int i = 0; i < binaryArray.length; i +=4) {
  target = 0;
  for (int j = 0; j < 4; j++) {
	target += (((int) binaryArray[i + j]) & 0xFF)<< (3 - j) * 8;  
  }  
  ...
}
```

## 느낀점

Unsigned type의 사용 이유를 다시 한 번 생각하게 되었다. 어차피 모든 연산은 signed type에서 처리할 수 있다(같은 type 과의 연산에서). unsigned의 이유는 연산과정에서 편의를 위한 것인지도 모르겠다. 사실 이건 매우 오만한 발언이다. 조금 더 unsigned에 관한 공부를 하고 다시 고슬링의 말을 생각해야겠다.

## 부록: Unsigned로 캐스팅하기

```byte, short, int``` type의 unsigned type으로 캐스팅을 소개로 글을 마치고자한다. 

사실 이것은 unsigned 캐스팅이라고 볼 수는 없고 해당 type보다 한 단계 높은 type에 값을 저장하는 것이다. (그래서 long의 경우를 제외하고 소개한다.) 프로젝트에서 표현해야 할 값이 해당 type보다 크다면 그냥 한 단계 더 큰 type을 쓰는 걸 추천한다. 

### 공통 두 줄 요약

1.  한 단계 높은 type으로 캐스팅한다.
2.  캐스팅한 값에 원래 type의 bit부분을 제외하고 0으로 마스킹한다.

### byte (8 bits)

```java
/**
* b:			byte
* unsignedByte:	short
*/
unsignedByte = (short) b;
unsignedByte = unsignedByte & 0xFF;
```

### short (16 bits)

```java
/**
* s:				short
* unsignedShort:	int
*/
unsignedShort = (int) s;
unsignedShort = unsignedShort & 0xFFFF;
```

### int (32 bits)

```java
/**
* i:				int
* unsignedInt:		long
*/
unsignedInt = (long) s;
unsignedInt = unsignedInt & 0xFFFFFFFF;
```

## 출처
https://stackoverflow.com/questions/9578639/best-way-to-convert-a-signed-integer-to-an-unsigned-long