# 변수
## 1 변수의 명명규칙
1. 대소문자 구분, 길이 제한 X
2. 예약어 사용 X
3. 숫자 시작 X
4. 특수문자는 \_와 "$"만 허용
5. 클래스 이름의 시작은 항상 대문자
6. 여러 단어로 이루어진 이름은 단어의 시작을 대문자로
7. 상수의 이름은 모두 대문자로, 여러 단어인 경우 \_로 구분


## 2 변수의 타입
### 2.1 기본형(8개)
| 분류   | 타입(byte)                   |
| ------ | ---------------------- |
| 논리형 | boolean(1)                |
| 문자형 | char(2)                   |
| 정수형 | byte(1), short(2), **int**(4), long(8) |
| 실수형 | float(4), **double**(8)          |

*boolean을 제외한 나머지 기본형은 서로 연산과 변환이 가능*

## 3 상수와 리터럴
### 3.1 상수(constant)
값을 한번 저장하면 변경할 수 없는 저장공간

	final int MAX_SPEED = 10;

* 선언과 동시에 초기화
* 변경 불가

### 3.2 리터럴(literal)
그 자체로 값을 의미

	int year//변수 = 2022;//리터럴

#### 3.2.1 리터럴의 타입과 접미사
| 종류   | 접미사 |
| ------ | ------ |
| long   | l, L   |
| float  | f, F   |

### 3.3 형식화된 출력

| 지시자 | 설명                           |
| ------ | ------------------------------ |
| %b     | 불리언(**b**oolean)            |
| %d     | 10진(**d**ecimal)              |
| %o     | 8진(**o**ctal)                 |
| %x, %X | 16진(he**x**a-decimal)         |
| %f     | 부동소수점(**f**loating-point) |
| %e, %E | 지수(**e**xponent)             |
| %s     | 문자열(**s**tring)             |

## 4 기본형
### 4.1 논리형
```java
boolean power = ture;
```
* 기본값 false

### 4.2 문자형
```java
char ch = 'A';
char ch = 65; // 동일한 문장
```
* 단 하나의 문자만 저장
* 문자의 유니코드(정수)로 저장

### 4.3 정수형
| 타입  | bit | byte |
| ----- | --- | ---- |
| byte  | 8   | 1    |
| short | 16  | 2    |
| int   | 32  | 4    |
| long  | 64  | 8    |

#### 4.3.1 정수형의 선택기준
* JVM의 피연산자 스택(operand stack)이 피연산자를 4byte 단위로 저장하기 때문에 int 형으로 사용하는 것이 더 효율적
* 정수형 변수 선언 -> int
* int의 범위(약 +-20억)을 넘어서면 long 사용
* byte, short는 성능보다 저장공간을 절약하는 것이 중요할 때 사용

### 4.4 실수형
#### 4.4.1 실수형의 범위와 정밀도
| 타입   | 정밀도 | bit | byte |
| ------ | ------ | --- | ---- |
| float  | 7자리  | 32  | 4    |
| double | 15자리 | 64  | 8     |

높은 정밀도가 필요하다면 double 사용

#### 4.4.2 실수형의 저장방식
float
| 부호 S(1) | 지수 E(8) | 가수 M(23) |
| --------- | --------- | ---------- |

double
| 부호 S(1) | 지수 E(11) | 가수 M(52) |
| --------- | ---------- | ---------- |

## 5 형변환
	(타입)피연산자

* 변수의 값은 형변환 후에도 변화 x
* 기본형에서 boolean을 제외한 나머지 타입들은 서로 형변환 가능
* 실수형 -> 정수형 변환 시 소수점 이하 값 버림

### 5.1 정수형간의 형변환
* 큰 타입 -> 작은 타입 : 값 손실 가능
* 작은 타입 -> 큰 타입 : 값 유지
* **음수의 경우, 빈 공간을 1로 채워 2의 보수 적용**

### 5.2 실수형 간의 형변환
#### 5.2.1 작은 타입 -> 큰 타입

| 지수(E)                                  | 가수(M) |
| ---------------------------------------- | ------- |
| -127(float의 기저) + 1023(double의 기저) | 0으로 채움        |

#### 5.2.2 큰 타입 -> 작은 타입

| 지수(E)                                  | 가수(M) |
| ---------------------------------------- | ------- |
| -1023(double의 기저) + 127(float의 기저) | 52자리 -> 23자리        |

* 가수의 24자리가 1이면 반올림 발생
* float보다 큰 값을 float으로 형변환 하는 경우, +-무한대/+-0의 값

### 5.3 자동 형변환
**기존의 값을 최대한 보존할 수 있는 타입으로 자동 형변환**
* 표현 범위가 좁은 타임에서 넓은 타입으로 형변환 하는 경우: 좁은 타입 -> 넓은 타입
* boolean을 제외한 나머지 7개의 기본형은 서로 형변환이 가능
* 기본형과 참조형은 서로 형변환 x
* 서로 다른 타입의 변수간의 연산은 형변환이 원칙, 값의 범위가 작은 타입 -> 넓은 타입은 생략 가능