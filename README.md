# 3. Type의 종류
<br>
<aside>
💡 자바스크립트에는 없는 타입스크립트만의 고유한 개념 중 가장 핵심이 되는 것은 타입이다. 
타입스크립트와 자바스크립트는 서로 호환되어야 한다. 이를 위해 타입스크립트는 자바스크립트가 사용하는 타입은 물론 타입스크립트의 타입도 사용할 수 있게 제공하고 있다.

<br>

</aside>

## **3.1 자바스크립트와 타입스크립트의 기본 타입**

| 타입의 종류 | JavaScript | TypeScript |
| --- | --- | --- |
| 수 | Number | number |
| 불리언 | Boolean | boolean |
| 문자열 | String | string |
| 객체 | Object | object |

타입스크립트는 기본적으로 다음과 같은 타입을 가지고 있다.

<br>

> 예제 3-1
> 

```tsx
boolean

number

string

object

array

tuple

enum

any // 모든 타입을 허용. 정해지지 않은 변수 지정 가능.

void // 값이 없음

null

undefined

unknown

never // 도달이 불가능한 코드

```

이 타입들로 자바스크립트의 변수, 함수 따위의 코드에 타입을 정의할 수 있다.

<br>

## **3.2 변수 타입선언**

자바스크립트에서는 문자열인 타입의 변수를 숫자 타입으로 변경하는 것이 가능하다. 자바스크립트에서 let으로 선언한 변수는 해당 코드에서 그 값이 언제든 변경될 수 있음을 암시한다.

반면, 타입스크립트는 타입 변환이 불가능하다.

자바스크립트는 런타임 도중에 변수 타입이 변경되었을 때 오류가 발생하지 않는데, 타입스크립트는 타입을 강제적으로 선언해 줌으로써 런타임이 아닌 컴파일러 단계에서 오류를 알 수 있다. 이는 생산성의 확실한 향상으로 이어진다.

<br>


### **3.2.1 기본적인 타입 표기**

타입스크립트에서는 변수를 선언한 후 콜론 뒤에 타입과 함께 세미콜론을 붙여준다. 이를 **타입주석**(type annotation)이라 한다.

<br>


> 예제 3-2
> 

```tsx
let name: string;

let age: number;
```

위처럼 타입주석을 통해 타입을 선언해준 변수는 선언된 타입과 다른 타입의 변수값으로 변경하려 하면 오류가 발생한다.

<br>


> 예제 3-3
> 

```tsx
let address: string = '제주';

let age: number = 28;

address = 0; // Error: The type 'number' is not assignable to type 'string'

age = '나이'; // Error!
```

<br>


### **3.2.2 타입추론**

타입 표기는 자바스크립트와의 호환성을 위해 생략될 수 있는데, 타입 선언이 없으면 컴파일러가 타입을 추론한다. 아래의 코드를 만나면 타입스크립트 컴파일러가 우측 값에 따라 타입을 지정해 준다.

이를 **타입추론**이라 한다.

<br>


> 예제 3-4
> 

```tsx
let a = true;    // a의 타입을 boolean으로 판단
let b = 'hello'; // b의 타입을 string으로 판단
let c = 1;       // c의 타입을 number로 판단
let d = {};      // d의 타입을 object로 판단

let name: string = "다은"; // 타입을 중복해서 지정
```

예제 3-4의 마지막 코드처럼, 타입스크립트 컴파일러가 타입을 유추할 수 있는 것에 중복하여 명시적으로 타입을 지정하는 것은 피해야 한다.

<br>


### **3.2.3 any**

any 타입은 모든 타입의 값을 지정할 수 있다. 숫자, 텍스트, 불린 값 또는 커스텀 타입(사용자가 정의한 타입) 값을 지정할 수 있다. 하지만 타입 체크를 확실히 하기 위해 any를 사용하는 것은 지양된다.

<br>


> 예제 3-5
> 

```tsx
// 모든 값 저장 가능
let a: any = 0;
a = true;
a = 'typescript';
a = {};
```

<br>


### **3.2.4 never 타입**

never 타입은 절대 반환을 하지 않는 함수에 사용된다. 도달되지 않는 코드를 나타내며 실행이 종료되지 않고 무한으로 반복되는 함수나 오류를 발생시키기 위해 존재하는 함수가 그 예가 될 수 있다.

<br>


> 예제 3-6
> 

```tsx
const neverTest = () => {
	while(true) {
		console.log("함수가 실행중입니다.)");
	}
}
```

위에서 neverTest함수의 타입은 never이다.

never의 또 다른 예시로 다음 함수를 살펴보자.

<br>


> 예제 3-7
> 

```tsx
function sayName(value: string): string {
		if(typeof value === "string") {
			return value;
		} else {
			return value;
		}
}
```

위의 코드에서 else 절의 value에 마우스를 올려 값을 확인해 보면  value : never라고 떠 never 타입임을 확인할 수 있다.

<br>


### **3.2.5 유니온타입**

하나의 변수에 지정할 수 있는 타입이 여러 개일 때 **유니온** 타입을 사용한다.  아래와 같이 선언한다.

<br>


> 예제 3-8
> 

```tsx
let a: string | number;
```

변수 a는 문자열과 숫자 타입만 허용한다. **any**로 써도 무방하지만 **유니온**으로 필요한 타입만을 지정해 주면 문자열과 숫자 그 외의 값이 들어올 경우 오류를 내보낸다. 예외 처리의 필요성이 사라진다.

💡 두 개 이상의 타입을 가지는 변수는 **any** 타입이 아닌 **유니온** 타입을 사용하는 것이 관습이다. 유니온을 사용하면 타입스크립트 컴파일러가 런타임 도중 잘못된 값이 지정될 경우 이를 감지해 오류를 바로 해결할 수 있다.

<br>


## **3.3 커스텀타입**

타입스크립트는 커스텀 타입을 만들 수 있다.  type 키워드를 사용하여 새로운 타입을 선언할 수 있고, 타입 별칭(type alias)를 사용하여 이미 존재하는 타입에 다른 이름을 붙여 사용할 수도 있다. 

학교에서 학생의 키와 몸무게를 기록하는 페이지를 만든다고 생각하고 키 **Centimeter**와 몸무게 **Kilogram**타입을 정의해 보자.

 

<br>


> 예제 3-9
> 

```tsx
type Centimeter = number;
type Kilogram = number;
```

위에서 정의한 타입을 가지고 학생을 나타내는 Student 타입을 만들어보자.

<br>


> 예제 3-10
> 

```tsx
type Student = {
	name: string;
	height: Centimeter;
	weight: Kilogram;
}
```

height에는 Centimeter 타입의 별칭을 사용하였고, weight에는 Kilogram 타입의 별칭을 사용해 Student 타입을 선언해 주었다.

다음으로 변수를 만들어 Student 타입을 추가해 주어 초기화한다. 

리터럴 표기법으로 인스턴스 student를 만들었다.

<br>


> 예제 3-11
> 

```tsx
let student: Student = {
	name: 'daeun',
	height: 163,
	weight: 53
}
```

만약 student 변수를 초기화할 때 프로퍼티 값이 누락된다면 아래와 같은 메시지가 뜬다.

해당 프로퍼티가 필수가 아닌 선택사항이라면, 타입을 만들 때 프로퍼티 이름 뒤에 물음표를 붙여 해당 프로퍼티가 조건부 프로퍼티임을 선언해 준다. 

<br>

> 예제 3-12
```tsx
>// 프로퍼티 누락
let student: Student = {
	height: 163,
	weight: 53
}
// Property 'name' is missing in type '{ height: number; weight: number; }' but required in type 'Student'.

type Student = {
	name? : string;   // 선택사항
	height : Centimeter;
	weight : Kilogram;
}
// name은 선택사항이 됨. 변수 student는 name 없이 초기화.
let student: Student = {
	height: 163,
	weight: 53
}
```