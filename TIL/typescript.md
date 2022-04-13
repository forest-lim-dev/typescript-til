# type script 기초
## 블로그를 보며
- https://heropy.blog/2020/01/27/typescript/

# 타입 기본(Types)
## 타입 지정
- 타입 스크립트는 일반 변수, 매개 변수(parameters), 객체 속성(Property) 등에 `: TYPES`과 같은 형태로 타입을 지정할 수 있음
```typescript
function someFunc(a: TYPE_A, b: TYPE_B): TYPE_RETURN {
    return a + b;
}
let some: TYPE_SOME = someFunc(1, 2)
```
- 다음 예시를 보면, add함수의 매개 변수 a와 b는 number타입이어 한다고 지정했고, 그렇게 실행된 함수의 반환값은 숫자로 추론(Inference)되기 때문에
- 변수 sum도 number타입이어야 한다고 지정했다.
```typescript
function add(a: number, b: number) {
    return a + b;
}
const sum: number = add(1,2);
console.log(number);
```

## 타입 에러
```typescript
function add(a: number, b: number) {
    return a + b;
}

const sum: string = add(1, 2);
console.log(sum);
```

## 타입 선언
### 불린(Boolean)
```typescript
let isBoolean: boolean;
let isDone: boolean = false;
```

### 숫자
- 모든 부동 소수점 값을 사용할 수 있습니다.
- ES6에 도입된 2진수 및 8진수 리터럴도 지원합니다.

```typescript
let num: number;
let integer: number = 6;
let float: number = 3.14;
let hex: number = 0xf00d; // 61453
let binary: number = 0b1010; // 10
let octal: number = 0o744; // 484
let infinity: number = Infinity;
let nan: number = NaN;
```

### 문자열
- 문자열을 나타냅니다. 
- 작은따옴표('), 큰따옴표(") 뿐만 아니라 ES6의 템플릿 문자열도 지원합니다.

```typescript
let str: string;
let red: string = 'Red';
let green: string = "Green";
let myColor: string = `My color is ${red}.`;
let yourColor: string = 'Your color is' + green;
```

### 배열: Array
- 순차적으로 값을 가지는 일반 배열을 나타냅니다.
- 배열은 다음과 같이 두 가지 방법으로 타입을 선언할 수 있습니다.
```typescript
// 문자열만 가지는 배열
let fruits: string[] = ['Apple', 'Banana', 'Mango'];
// Or
let fruits: Array<string> = ['Apple', 'Banana', 'Mango'];

// 숫자만 가지는 배열
let oneToSeven: number[] = [1, 2, 3, 4, 5, 6, 7];
// Or
let oneToSeven: Array<number> = [1, 2, 3, 4, 5, 6, 7];

// 유니언 타입(다중 타입)의 ‘문자열과 숫자를 동시에 가지는 배열’도 선언할 수 있습니다.
let array: (string | number)[] = ['Apple', 1, 2, 'Banana', 'Mango', 3];
// Or
let array: Array<string | number> = ['Apple', 1, 2, 'Banana', 'Mango', 3];

// 인터페이스(Interface)나 커스텀 타입(Type)을 사용할 수도 있습니다.
interface IUser {
    name: string,
    age: number,
    isValid: boolean
}
let userArr: IUser[] = [
    {
        name: 'Neo',
        age: 85,
        isValid: true
    },
    {
        name: 'Lewis',
        age: 52,
        isValid: false
    },
    {
        name: 'Evan',
        age: 36,
        isValid: true
    }
];

// 읽기전용으로 선언하는 경우
let arrA: readonly number[] = [1, 2, 3, 4];
let arrB: ReadonlyArray<number> = [0, 9, 8, 7];

arrA[0] = 123; // Error - TS2542: Index signature in type 'readonly number[]' only permits reading.
arrA.push(123); // Error - TS2339: Property 'push' does not exist on type 'readonly number[]'.

arrB[0] = 123; // Error - TS2542: Index signature in type 'readonly number[]' only permits reading.
arrB.push(123); // Error - TS2339: Property 'push' does not exist on type 'readonly number[]'.
```

### 튜플
- Tuple 타입은 배열과 매우 유사합니다.
- 차이점이라면 정해진 타입의 고정된 길이(length) 배열을 표현합니다.

```typescript
let tuple: [string, number];
tuple = ['a', 1];
tuple = ['a', 1, 2]; // Error - TS2322
tuple = [1, 'a']; // Error - TS2322

// variables
let userId: number = 1234;
let userName: string = 'HEROPY';
let isValid: boolean = true;

// Tuple
let user: [number, string, boolean] = [1234, 'HEROPY', true];
console.log(user[0]); // 1234
console.log(user[1]); // 'HEROPY'
console.log(user[2]); // true

// 나아가 2차원 배열로 선언해서 사용하는 것도 가능하다.
let users: [number, string, boolean][];
// Or
// let users: Array<[number, string, boolean]>;
users = [[1, 'Neo', true], [2, 'Evan', false], [3, 'Lewis', true]];

// 배열에서 사용한 것과 같이 readonly 키워드를 사용해 읽기 전용 튜플을 생성할 수도 있습니다.
let a: readonly [string, number] = ['Hello', 123];
a[0] = 'World'; // Error - TS2540: Cannot assign to '0' because it is a read-only property.
```

### 열거형(enum)
- Enum은 숫자 혹은 문자열 값 집합에 이름(Member)을 부여할 수 있는 타입으로, 값의 종류가 일정한 범위로 정해져 있는 경우 유용합니다.
- 기본적으로 0부터 시작하며 값은 1씩 증가합니다.
- 0부터 시작하는데 값이 할당된 곳부터 1씩 증가하는 형태
```typescript
enum Week {
  Sun,
  Mon,
  Tue = 11,
  Wed,
  Thu,
  Fri,
  Sat
}

console.log(Week);
console.log(Week.Sun); // 0
console.log(Week['Sun']); // 0
console.log(Week[0]); // 'Sun'

// 숫자 뿐만 아니라 문자도 가능
enum Color {
    Red = 'red',
    Green = 'green',
    Blue = 'blue'
}
console.log(Color.Red); // red
console.log(Color['Green']); // green
```

### 모든 타입: Any
- Any는 모든 타입을 의미합니다.
- 따라서 일반적인 자바스크립트 변수와 동일하게 어떤 타입의 값도 할당할 수 있습니다.
- 외부 자원을 활용해 개발할 때 불가피하게 타입을 단언할 수 없는 경우, 유용할 수 있습니다.

```typescript
let any: any = 123;
any = 'Hello world';
any = {};
any = null;

const list: any[] = [1, true, 'Anything!'];
```

### 알 수 없는 타입: Unknown
- Any와 같이 최상위 타입인 Unknown은 알 수 없는 타입을 의미합니다.
- Any와 같이 Unknown에는 어떤 타입의 값도 할당할 수 있지만, Unknown을 다른 타입에는 할당할 수 없습니다.

>> 일반적인 경우 Unknown은 타입 단언(Assertions)이나 타입 가드(Guards)를 필요로 합니다.
>> 타입 단언이나 가드에 대한 내용은 다른 파트에서 정리합니다.

```typescript
let a: any = 123;
let u: unknown = 123;

let v1: boolean = a; // 모든 타입(any)은 어디든 할당할 수 있습니다.
let v2: number = u; // 알 수 없는 타입(unknown)은 모든 타입(any)을 제외한 다른 타입에 할당할 수 없습니다.
let v3: any = u; // OK!
let v4: number = u as number; // 타입을 단언하면 할당할 수 있습니다.

type Result = {
    success: true,
    value: unknown
} | {
    success: false,
    error: Error
}

export default function getItems(user: IUser): Result {
    // Some logic...
    if (id.isValid) {
        return {
            success: true,
            value: ['Apple', 'Banana']
        };
    } else {
        return {
            success: false,
            error: new Error('Invalid user.')
        }
    }
}
```

### 객체: Object
- 기본적으로 `typeof` 연산자가 `"object"`로 반환하는 모든 타입을 나타냅니다.
> 컴파일러 옵션에서 엄격한 타입 검사(strict)를 true로 설정하면, null은 포함하지 않습니다.

```typescript
let obj: object = {};
let arr: object = [];
let func: object = function () {};
let nullValue: object = null;
let date: object = new Date();
// ...

// 여러 타입의 상위 타입이기 때문에 그다지 유용하지 않습니다.
// 보다 정확하게 타입 지정을 하기 위해 다음과 같이 객체 속성(Properties)들에 대한 타입을 개별적으로 지정할 수 있습니다.
let userA: { name: string, age: number } = {
    name: 'HEROPY',
    age: 123
};

let userB: { name: string, age: number } = {
    name: 'HEROPY',
    age: false, // Error
    email: 'thesecon@gmail.com' // Error
};
```
```typescript
// 반복적인 사용을 원하는 경우 -> interface나 type을 사용
interface IUser {
    name: string,
    age: number
}

let userA: IUser = {
    name: 'HEROPY',
    age: 123
};

let userB: IUser = {
    name: 'HEROPY',
    age: false, // Error
    email: 'thesecon@gmail.com' // Error
};
```

### Null과 undefined
- 기본적으로 Null과 Undefined는 모든 타입의 하위 타입으로, 다음과 같이 각 타입에 할당할 수 있습니다.
- 심지어 서로의 타입에도 할당 가능합니다.
```typescript
let num: number = undefined;
let str: string = null;
let obj: { a: 1, b: false } = undefined;
let arr: any[] = null;
let und: undefined = null;
let nul: null = undefined;
let voi: void = null;
```
- 이는 컴파일 옵션 `"strictNullChecks": true`을 통해 엄격하게 `Null과` `Undefined` 서로의 타입까지 더 이상 할당할 수 없게 합니다.

### Void
- Void는 일반적으로 값을 반환하지 않는 함수에서 사용합니다.
- `: void` 위치는 함수가 반환 타입을 명시하는 곳입니다.
```typescript
function hello(msg: string): void {
  console.log(`Hello ${msg}`);
}
```
- 값을 반환하지 않는 함수는 실제로 undefined를 반환
```typescript
function hello(msg: string): void {
  console.log(`Hello ${msg}`);
}
const hi: void = hello('world'); // Hello world
console.log(hi); // undefined
```

### Never
- Never은 절대 발생하지 않을 값을 나타내며, 어떠한 타입도 적용할 수 없습니다.
```typescript
function error(message: string): never {
  throw new Error(message);
}

const never: [] = [];
never.push(3); // Error - TS2345: Argument of type '3' is not assignable to parameter of type 'never'.
```

### 유니언(Union)
- 2개 이상의 타입을 허용하는 경우, 이를 유니언(Union)이라고 합니다.
- `|`(vertical bar)를 통해 타입을 구분하며, `()`는 선택 사항입니다.
```typescript
let union: (string | number);
union = 'Hello type!';
union = 123;
union = false; // Error - TS2322: Type 'false' is not assignable to type 'string | number'.
```

### 인터섹션(Intersection)
- `&`(ampersand)를 사용해 2개 이상의 타입을 조합하는 경우, 이를 인터섹션(Intersection)이라고 합니다.
- 인터섹션은 새로운 타입을 생성하지 않고 기존의 타입들을 조합할 수 있기 때문에 유용하지만, 자주 사용되는 방법은 아닙니다.
> 위에서 살펴본 유니언을 마치 ‘또는(Or)’과 같이 이해할 수 있다면, 인터섹션은 ‘그리고(And)’와 같이 이해할 수 있습니다.
```typescript
// 기존 타입들이 조합 가능하다면 인터섹션을 활용할 수 있습니다.
interface IUser {
  name: string,
  age: number
}
interface IValidation {
  isValid: boolean
}
const heropy: IUser = {
  name: 'Heropy',
  age: 36,
  isValid: true // Error -  TS2322: Type '{ name: string; age: number; isValid: boolean; }' is not assignable to type 'IUser'.
};
const neo: IUser & IValidation = {
  name: 'Neo',
  age: 85,
  isValid: true
};

// 혹은 기존 타입(IUser, IValidation)과 비슷하지만, 정확히 일치하는 타입이 없다면 새로운 타입을 생성해야 합니다.
interface IUserNew {
  name: string,
  age: number,
  isValid: boolean
}
const evan: IUserNew = {
  name: 'Evan',
  age: 36,
  isValid: false
};
```

### 함수
- 화살표 함수를 이용해 타입을 지정할 수 있습니다. 
- 인수의 타입과 반환 값의 타입을 입력합니다.

```typescript
// myfunc는 2개의 숫자 타입 인수를 주고, 숫자 타입을 반환하는 함수
let myfunc: (arg1: number, arg2: number) => number;
myfunc = function(x, y) {
    return x + y;
}

// 인수가 없고, 반환도 없는 경우
let yourFunc: () => void;
yourFunc() = function() {
    console.log("hello world~")
};
```

### 타입추론
- 명시적으로 타입 선언이 되어있지 않은 경우, 타입스크립트는 타입을 추론해 제공합니다.
- 개념은 매우 단순합니다.
```typescript
let num = 12;
num = 'Hello type!'; // TS2322: Type '"Hello type!"' is not assignable to type 'number'.
```
- 이렇게 타입스크립트가 타입을 추론하는 경우는 다음과 같습니다.
  - 초기화된 변수 
  - 기본값이 설정된 매개 변수 
  - 반환 값이 있는 함수

```typescript
// 초기화된 변수 `num`
let num = 12;

// 기본값이 설정된 매개 변수 `b`
function add(a: number, b: number = 2): number {
  // 반환 값(`a + b`)이 있는 함수
  return a + b;
}
```

> 타입 추론이 엄격하지 않은 타입 선언을 의미하는 것은 아닙니다. 따라서 이를 활용해 모든 곳에 타입을 명시할 필요는 없으며, 많은 경우 더 좋은 코드 가독성을 제공할 수 있습니다.

### 타입단언(Assertions)
- 타입스크립트가 타입 추론을 통해 판단할 수 있는 타입의 범주를 넘는 경우, 더 이상 추론하지 않도록 지시할 수 있습니다.
- 이를 ‘타입 단언’이라고 하며, 이는 프로그래머가 타입스크립트보다 타입에 대해 더 잘 이해하고 있는 상황을 의미합니다.
```typescript
function someFunc(val: string | number, isNumber: boolean) {
  // some logics
  if (isNumber) {
    val.toFixed(2); // Error - TS2339: ... Property 'toFixed' does not exist on type 'string'.
  }
}
```
- 함수의 매개 변수 val은 유니언 타입으로 문자열(String)이거나 숫자(Number)일 수 있습니다. 
- 그리고 매개 변수 isNumber는 불린(Boolean)이며, 이름을 통해 숫자 여부를 확인하는 값이라는 것을 (우리는) 추론할 수 있습니다. 
- 따라서 우리는 isNumber가 true일 경우 val은 숫자일 것이고, 이에 toFixed를 사용할 수 있음을 확실히 알 수 있습니다. 
- 하지만 타입스크립트는 ‘isNumber’라는 이름만으로 위 내용을 추론할 수 없기 때문에 “val이 문자열인 경우 toFixed를 사용할 수 없다”고 (컴파일 단계에서) 다음과 같은 에러를 반환합니다.
- 따라서 우리는 isNumber가 true일 때 val이 숫자임을 다음과 같이 2가지 방식으로 단언할 수 있습니다. 
- 두 번째 방식(<number>val)은 JSX를 사용하는 경우 특정 구문 파싱에서 문제가 발생할 수 있으며, 결과적으로 .tsx 파일에서는 전혀 사용할 수 없습니다.

```typescript
function someFunc(val: string | number, isNumber: boolean) {
  // some logics
  if (isNumber) {
    // 1. 변수 as 타입
    (val as number).toFixed(2);
    // Or
    // 2. <타입>변수
    // (<number>val).toFixed(2);
  }
}
```

### Non-null 단언연산자
- !를 사용하는 Non-null 단언 연산자(Non-null assertion operator)를 통해 피연산자가 Nullish(null이나 undefined) 값이 아님을 단언할 수 있는데, 변수나 속성에서 간단하게 사용할 수 있기 때문에 유용합니다.
```typescript
// Error - TS2533: Object is possibly 'null' or 'undefined'.
function fnA(x: number | null | undefined) {
  return x.toFixed(2);
}

// if statement
function fnD(x: number | null | undefined) {
  if (x) {
    return x.toFixed(2);
  }
}

// Type assertion
function fnB(x: number | null | undefined) {
  return (x as number).toFixed(2);
}
function fnC(x: number | null | undefined) {
  return (<number>x).toFixed(2);
}

// Non-null assertion operator
function fnE(x: number | null | undefined) {
  return x!.toFixed(2);
}
```
- 다음 예제 중 fnA 함수를 살펴보면, 매개 변수 x는 함수 내에서 toFixed를 사용하는 숫자 타입으로 처리되지만 null이나 undefined일 수 있기 때문에 에러가 발생합니다.
- 이를 타입 단언이나 if 조건문으로 해결할 수도 있지만, 마지막 함수와 같이 !를 사용하는 Non-null 단언 연산자를 이용해 간단하게 정리할 수 있습니다.
- 특히 컴파일 환경에서 체크하기 어려운 DOM 사용에서 유용합니다.
- 물론 일반적인 타입 단언을 사용할 수도 있습니다.

```typescript
// Error - TS2531: Object is possibly 'null'.
document.querySelector('.menu-item').innerHTML;

// Type assertion
(document.querySelector('.menu-item') as HTMLDivElement).innerHTML;
(<HTMLDivElement>document.querySelector('.menu-item')).innerHTML;

// Non-null assertion operator
document.querySelector('.menu-item')!.innerHTML;
```

### 타입 가드(Guards)
- 다음 예제와 같이 `val`의 타입을 매번 보장하기 위해 타입 단언을 여러 번 사용하게 되는 경우가 있습니다.
```typescript
function someFunc(val: string | number, isNumber: boolean) {
  if (isNumber) {
    (val as number).toFixed(2);
    isNaN(val as number);
  } else {
    (val as string).split('');
    (val as string).toUpperCase();
    (val as string).length;
  }
}
```
- 이 경우 타입 가드를 제공하면 타입스크립트가 추론 가능한 특정 범위(scope)에서 타입을 보장할 수 있습니다.
- 타입 가드는 NAME is TYPE 형태의 타입 술부(Predicate)를 반환 타입으로 명시한 함수입니다.
- 다음 예제에서 타입 술부는 val is number입니다.
- 타입 단언이 없어지니 훨씬 깔끔합니다.

```typescript
function isNumber(val: string | number): val is number {
  return typeof val === 'number';
}

function someFunc(val: string | number) {
  if (isNumber(val)) {
    val.toFixed(2);
    isNaN(val);
  } else {
    val.split('');
    val.toUpperCase();
    val.length;
  }
}
```

- 위 방식뿐만 아니라 제공 가능한 타입 가드가 더 있습니다.
- `typeof`, `in` 그리고 `instanceof` 연산자를 직접 사용하는 타입 가드입니다.
- 비교적 단순한 로직에서 추천되는 방식입니다.

> `typeof` 연산자는 `number`, `string`, `boolean`, 그리고 `symbol`만 타입 가드로 인식할 수 있습니다. `in` 연산자의 우변 객체(`val`)는 `any` 타입이어야 합니다.

```typescript
// 기존 예제와 같이 `isNumber`를 제공(추상화)하지 않아도 `typeof` 연산자를 직접 사용하면 타입 가드로 동작합니다.
// https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/typeof
function someFuncTypeof(val: string | number) {
  if (typeof val === 'number') {
    val.toFixed(2);
    isNaN(val);
  } else {
    val.split('');
    val.toUpperCase();
    val.length;
  }
}

// 별도의 추상화 없이 `in` 연산자를 사용해 타입 가드를 제공합니다.
// https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/in
function someFuncIn(val: any) {
  if ('toFixed' in val) {
    val.toFixed(2);
    isNaN(val);
  } else if ('split' in val) {
    val.split('');
    val.toUpperCase();
    val.length;
  }
}

// 역시 별도의 추상화 없이 `instanceof` 연산자를 사용해 타입 가드를 제공합니다.
// https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/instanceof
class Cat {
  meow() {}
}
class Dog {
  woof() {}
}
function sounds(ani: Cat | Dog) {
  if (ani instanceof Cat) {
    ani.meow();
  } else {
    ani.woof();
  }
}
```

### 인터페이스(Interface)
- 인터페이스(Interface)는 타입스크립트 여러 객체를 정의하는 일종의 규칙이며 구조입니다.
- 다음과 같이 interface 키워드와 함께 사용합니다.
```typescript
interface IUser {
  name: string,
  age: number,
  isAdult: boolean
}

let user1: IUser = {
  name: 'Neo',
  age: 123,
  isAdult: true
};

// Error - TS2741: Property 'isAdult' is missing in type '{ name: string; age: number; }' but required in type 'IUser'.
let user2: IUser = {
  name: 'Evan',
  age: 456
};
```

- `:`(colon), `,`(comma) 혹은 기호를 사용하지 않을 수 있습니다.
```typescript
interface IUser {
  name: string,
  age: number
}
// Or
interface IUser {
  name: string;
  age: number;
}
// Or
interface IUser {
  name: string
  age: number
}
```

### 읽기전용속성(Readonly properties)
- `readonly` 키워드를 사용하면 초기화된 값을 유지해야 하는 읽기 전용 속성을 정의할 수 있습니다.
```typescript
interface IUser {
  readonly name: string,
  age: number
}

// 초기화
let user: IUser = {
  name: 'Neo',
  age: 36
};

user.age = 85; // Ok
user.name = 'Evan'; // Error - TS2540: Cannot assign to 'name' because it is a read-only property.
```

- 만약 모든 속성이 `readonly`일 경우, 유틸리티(Utility)나 단언(Assertion) 타입을 활용할 수 있습니다.

```typescript
// All readonly properties
interface IUser {
  readonly name: string,
  readonly age: number
}
let user: IUser = {
  name: 'Neo',
  age: 36
};
user.age = 85; // Error
user.name = 'Evan'; // Error


// Readonly Utility
interface IUser {
  name: string,
  age: number
}
let user: Readonly<IUser> = {
  name: 'Neo',
  age: 36
};
user.age = 85; // Error
user.name = 'Evan'; // Error


// Type assertion
let user = {
  name: 'Neo',
  age: 36
} as const;
user.age = 85; // Error
user.name = 'Evan'; // Error
```

### 함수타입
- 함수 타입을 인터페이스로 정의하는 경우, `호출 시그니처(Call signature)`라는 것을 사용합니다.
- `호출 시그니처`는 다음과 같이 함수의 `매개 변수(parameter)`와 `반환 타입`을 지정합니다.
```typescript
interface IName {
  (PARAMETER: PARAM_TYPE): RETURN_TYPE // Call signature
}
```

- 간단한 예시를 살펴봅시다.
- 인터페이스 IGetUser를 통해 함수 타입을 정의했으며, 이는 name 매개 변수를 하나 가지며(이름이 일치할 필요는 없습니다), IUser 타입을 반환해야 합니다.

```typescript
interface IUser {
  name: string
}
interface IGetUser {
  (name: string): IUser
}

// 매개 변수 이름이 인터페이스와 일치할 필요가 없습니다.
// 또한 타입 추론을 통해 매개 변수를 순서에 맞게 암시적 타입으로 제공할 수 있습니다.
const getUser: IGetUser = function (n) { // n is name: string
  // Find user logic..
  // ...
  return user;
};
getUser('Heropy');
```

### 클래스타입
- **인터페이스로 클래스를 정의하는 경우, `implements` 키워드를 사용합니다.**
```typescript
interface IUser {
  name: string,
  getName(): string
}

class User implements IUser {
  constructor(public name: string) {}
  getName() {
    return this.name;
  }
}

const neo = new User('Neo');
neo.getName(); // Neo
```

- 기본적인 사용법은 어렵지 않습니다.
- 그런데 만약 정의한 **클래스를 인수로 사용하는 경우** 다음과 같은 문제가 발생할 수 있습니다.
- 다음 예제에서 인터페이스 ICat은 호출 가능한 구조가 아니기 때문입니다.

```typescript
interface ICat {
  name: string
}

class Cat implements ICat {
  constructor(public name: string) {}
}

function makeKitten(c: ICat, n: string) {
  return new c(n); // Error - TS2351: This expression is not constructable. Type 'ICat' has no construct signatures.
}
const kitten = makeKitten(Cat, 'Lucy');
console.log(kitten);
```

- 이를 위해 `구성 시그니처(Construct signature)`를 제공할 수 있습니다.
- 구성 시그니처는 위에서 살펴본 호출 시그니처와 비슷하지만, new 키워드를 사용해야 합니다.

```typescript
interface IName {
  new (PARAMETER: PARAM_TYPE): RETURN_TYPE // Construct signature
}
```

- 위에서 봤던 예제를 다음과 같이 수정합니다.
- ICatConstructor라는 구성 시그니처를 가지는 호출 가능한 인터페이스를 정의하면, 문제없이 동작하는 것을 확인할 수 있습니다.

```typescript
interface ICat {
  name: string
}
interface ICatConstructor {
  new (name: string): ICat;
}

class Cat implements ICat {
  constructor(public name: string) {}
}

function makeKitten(c: ICatConstructor, n: string) {
  return new c(n); // ok
}
const kitten = makeKitten(Cat, 'Lucy');
console.log(kitten);
```

- 여러 재미있는 예제들
```typescript
interface IFullName {
  firstName: string,
  lastName: string
}
interface IFullNameConstructor {
  new(firstName: string): IFullName; // Construct signature
}


function makeSon(c: IFullNameConstructor, firstName: string) {
  return new c(firstName);
}
function getFullName(son: IFullName) {
  return `${son.firstName} ${son.lastName}`;
}


// Anderson family
class Anderson implements IFullName {
  public lastName: string;
  constructor (public firstName: string) {
    this.lastName = 'Anderson';
  }
}
const tomas = makeSon(Anderson, 'Tomas');
const jack = makeSon(Anderson, 'Jack');
getFullName(tomas); // Tomas Anderson
getFullName(jack); // Jack Anderson


// Smith family?
class Smith implements IFullName {
  public lastName: string;
  constructor (public firstName: string, agentCode: number) {
    this.lastName = `Smith ${agentCode}`;
  }
}
const smith = makeSon(Smith, 7); // Error - TS2345: Argument of type 'typeof Smith' is not assignable to parameter of type 'IFullNameConstructor'.
getFullName(smith);
```

### 인덱싱 가능 타입
- 우리는 인터페이스를 통해 특정 속성(메소드 등)의 타입을 정의할 순 있지만, 수많은 속성을 가지거나 단언할 수 없는 임의의 속성이 포함되는 구조에서는 기존의 방식만으론 한계가 있습니다. 
- 이런 상황에서 유용한 인덱스 시그니처(Index signature)에 대해서 살펴봅시다.
  - arr[2]와 같이 ‘숫자’로 인덱싱하거나 obj['name']과 같이 ‘문자’로 인덱싱하는, 인덱싱 가능 타입(Indexable types)들이 있습니다.
  - 이런 인덱싱 가능 타입들을 정의하는 인터페이스는 `인덱스 시그니처(Index signature)`라는 것을 가질 수 있습니다.
  - 인덱스 시그니처는 다음 구조와 같이, 인덱싱에 사용할 `인덱서(Indexer)의 이름`과 `타입` 그리고 `인덱싱 결과의 반환 값`을 지정합니다.
  - 인덱서의 타입은 `string과 number만 지정`할 수 있습니다.

```typescript
interface INAME {
  [INDEXER_NAME: INDEXER_TYPE]: RETURN_TYPE // Index signature
}
```
> 배열(객체)에서 위치를 가리키는 숫자(문자)를 인덱스(index)라고 하며, 각 배열 요소(객체 속성)에 접근하기 위하여 인덱스를 사용하는 것을 인덱싱(indexing)이라고 합니다.
> (배열을 구성하는 각각의 값은 배열 요소(element)라고 합니다)

- 이해를 돕기 위해 다음 예제를 살펴보면,
- 인터페이스 IItem은 인덱스 시그니처를 가지고 있으며, 그 IItem을 타입(인터페이스)으로 하는 item이 있고, 그 item을 item[0]이나 item[1]과 같이 숫자로 인덱싱할 때 반환되는 값은 'a'나 b' 같은 문자여야 합니다.
- item을 item['0']과 같이 문자로 인덱싱하는 경우 에러가 발생합니다.

```typescript
interface IItem {
  [itemIndex: number]: string // Index signature
}
let item: IItem = ['a', 'b', 'c']; // Indexable type
console.log(item[0]); // 'a' is string.
console.log(item[1]); // 'b' is string.
console.log(item['0']); // Error - TS7015: Element implicitly has an 'any' type because index expression is not of type 'number'.
```

- 참고로 인덱싱 결과의 반환 타입으로 유니온을 사용하면 다음과 같이 활용할 수 있습니다.

```typescript
interface IItem {
  [itemIndex: number]: string | boolean | number[]
}
let item: IItem = ['Hello', false, [1, 2, 3]];
console.log(item[0]); // Hello
console.log(item[1]); // false
console.log(item[2]); // [1, 2, 3]
```

- 이번에는 문자로 인덱싱하는 예제를 살펴봅시다.
- 인터페이스 IUser는 인덱스 시그니처를 가지고 있으며, 그 IUser를 타입(인터페이스)로 하는 user가 있고, 
- 그 user를 user['name'], user['email'] 또는 user['isValid']와 같이 문자로 인덱싱할 때 반환되는 값은 'Neo'나 'thesecon@gmail.com' 같은 문자 혹은 true 같은 불린이어야 합니다.
- 또한 user[0]과 같은 숫자로 인덱싱하는 경우나 user['0']과 같이 문자로 인덱싱하는 경우 모두 인덱싱 전에 숫자가 문자열로 변환되기 때문에 다음과 같이 값을 반환할 수 있습니다.

```typescript
interface IUser {
  [userProp: string]: string | boolean
}
let user: IUser = {
  name: 'Neo',
  email: 'thesecon@gmail.com',
  isValid: true,
  0: false
};
console.log(user['name']); // 'Neo' is string.
console.log(user['email']); // 'thesecon@gmail.com' is string.
console.log(user['isValid']); // true is boolean.
console.log(user[0]); // false is boolean
console.log(user[1]); // undefined
console.log(user['0']); // false is boolean
```

- 인덱스 시그니처를 사용하면 다음 예제와 같이 인터페이스에 정의되지 않은 속성들을 사용할 때 유용합니다.
- 단, 해당 속성이 인덱스 시그니처에 정의된 반환 값을 가져야 함에 주의해야 합니다.
- 다음 예제에서 isAdult 속성은 정의된 string이나 number 타입을 반환하지 않지 않기 때문에 에러가 발생합니다.
```typescript
interface IUser {
  [userProp: string]: string | number
  name: string,
  age: number
}
let user: IUser = {
  name: 'Neo',
  age: 123,
  email: 'thesecon@gmail.com',
  isAdult: true // Error - TS2322: Type 'true' is not assignable to type 'string | number'.
};
console.log(user['name']); // 'Neo'
console.log(user['age']); // 123
console.log(user['email']); // thesecon@gmail.com
```

### keyof
- 인덱싱 가능 타입에서 keyof를 사용하면 속성 이름을 타입으로 사용할 수 있습니다.
- 인덱싱 가능 타입의 속성 이름들이 유니온 타입으로 적용됩니다.
- 간단한 예제를 살펴보겠습니다.

```typescript
interface ICountries {
  KR: '대한민국',
  US: '미국',
  CP: '중국'
}
let country: keyof ICountries; // 'KR' | 'US' | 'CP'
country = 'KR'; // ok
country = 'RU'; // Error - TS2322: Type '"RU"' is not assignable to type '"KR" | "US" | "CP"'.
```

### 인터페이스 확장
- 인터페이스도 클래스처럼 extends 키워드를 활용해 상속할 수 있습니다.
```typescript
interface IAnimal {
  name: string
}
interface ICat extends IAnimal {
  meow(): string
}

class Cat implements ICat { // Error - TS2420: Class 'Cat' incorrectly implements interface 'ICat'. Property 'name' is missing in type 'Cat' but required in type 'ICat'.
  meow() {
    return 'MEOW~'
  }
}
```

- 그리고 같은 이름의 인터페이스를 여러 개 만들 수도 있습니다.(기존에 만들어진 인터페이스에 내용을 추가하는 경우에 유용합니다.)

```typescript
interface IFullName {
  firstName: string,
  lastName: string
}
interface IFullName {
  middleName: string
}

const fullName: IFullName = {
  firstName: 'Tomas',
  middleName: 'Sean',
  lastName: 'Connery'
};
```

### 타입 별칭(type aliases)
- `type` 키워드를 사용해 새로운 타입 조합을 만들 수 있습니다.
- 하나 이상의 타입을 조합해 별칭(이름)을 부여하며, 정확히는 조합한 각 타입들을 참조하는 별칭을 만드는 것입니다.
- 일반적인 경우 둘 이상의 조합으로 구성하기 위해 `유니온`을 많이 사용합니다.

```typescript
type MyType = string;
type YourType = string | number | boolean;
type TUser = {
  name: string,
  age: number,
  isValid: boolean
} | [string, number, boolean];

let userA: TUser = {
  name: 'Neo',
  age: 85,
  isValid: true
};
let userB: TUser = ['Evan', 36, false];

function someFunc(arg: MyType): YourType {
  switch (arg) {
    case 's':
      return arg.toString(); // string
    case 'n':
      return parseInt(arg); // number
    default:
      return true; // boolean
  }
}
```

### 제네릭
- `Generic`은 재사용을 목적으로 함수나 클래스의 선언 시점이 아닌, 사용 시점에 타입을 선언할 수 있는 방법을 제공합니다.
> 타입을 인수로 받아서 사용한다고 이해하면 쉽습니다.

다음 예제는 `toArray` 함수가 인수로 받은 값을 배열로 반환하도록 작성되었습니다.
매개 변수가 Number 타입만 허용하기 때문에 String 타입을 인수로 하는 함수 호출에서 에러가 발생합니다.
```typescript
function toArray(a: number, b: number): number[] {
  return [a, b];
}
toArray(1, 2);
toArray('1', '2'); // Error - TS2345: Argument of type '"1"' is not assignable to parameter of type 'number'.
```

- 조금 더 범용적으로 만들기 위해 유니언 방식을 사용했습니다.
- 이제 String 타입을 인수로 받을 수 있지만, 가독성이 떨어지고 새로운 문제도 발생했습니다.
- 세 번째 호출을 보면 의도치 않게 Number와 String 타입을 동시에 받을 수 있게 되었습니다.

```typescript
function toArray(a: number | string, b: number | string): (number | string)[] {
  return [a, b];
}
toArray(1, 2); // Only Number
toArray('1', '2'); // Only String
toArray(1, '2'); // Number & String
```

- 이번에는 `Generic`을 사용합니다.
- 함수 이름 우측에 `<T>`를 작성해 시작합니다.
- T는 타입 변수(Type variable)로 사용자가 제공한 타입으로 변환될 식별자입니다.
- 이제 세 번째 호출은 의도적으로 Number와 String 타입을 동시에 받을 수 있습니다.(혹은 유니언을 사용하지 않으면 에러가 발생합니다)

```typescript
function toArray<T>(a: T, b: T): T[] {
  return [a, b];
}

toArray<number>(1, 2);
toArray<string>('1', '2');
toArray<string | number>(1, '2');
toArray<number>(1, '2'); // Error
```

- 타입 추론을 활용해, 사용 시점에 타입을 제공하지 않을 수 있습니다.
```typescript
function toArray<T>(a: T, b: T): T[] {
  return [a, b];
}

toArray(1, 2);
toArray('1', '2');
toArray(1, '2'); // Error
```

### 제약조건(Constraints)
- 인터페이스나 타입 별칭을 사용하는 제네릭을 작성할 수도 있습니다.
- 다음 예제는 별도의 제약 조건(Constraints)이 없어서 모든 타입이 허용됩니다.
```typescript
interface MyType<T> {
  name: string,
  value: T
}

const dataA: MyType<string> = {
  name: 'Data A',
  value: 'Hello world'
};
const dataB: MyType<number> = {
  name: 'Data B',
  value: 1234
};
const dataC: MyType<boolean> = {
  name: 'Data C',
  value: true
};
const dataD: MyType<number[]> = {
  name: 'Data D',
  value: [1, 2, 3, 4]
};
```

- 만약 타입 변수 T가 string과 number인 경우만 허용하려면 아래 예제와 같이 `extends` 키워드를 사용하는 제약 조건을 추가할 수 있습니다.
- 기본 문법은 다음과 같습니다.(`T extends U`)
```typescript
interface MyType<T extends string | number> {
  name: string,
  value: T
}

const dataA: MyType<string> = {
  name: 'Data A',
  value: 'Hello world'
};
const dataB: MyType<number> = {
  name: 'Data B',
  value: 1234
};
const dataC: MyType<boolean> = { // TS2344: Type 'boolean' does not satisfy the constraint 'string | number'.
  name: 'Data C',
  value: true
};
const dataD: MyType<number[]> = { // TS2344: Type 'number[]' does not satisfy the constraint 'string | number'.
  name: 'Data D',
  value: [1, 2, 3, 4]
};
```

- 대표적으로 type과 interface 키워드를 사용하는 타입 선언은 
- 다음 예제와 같이 = 기호를 기준으로 ‘식별자’와 ‘타입 구현’으로 구분할 수 있습니다. 
- 제약 조건은 ‘식별자’ 영역에서 사용하는 extends에 한합니다.

### 조건부타입(Conditional Types)
- 대표적으로 type과 interface 키워드를 사용하는 타입 선언은 다음 예제와 같이 `=` 기호를 기준으로 ‘`식별자`’와 ‘`타입 구현`’으로 구분할 수 있습니다.
- 제약 조건은 ‘식별자’ 영역에서 사용하는 extends에 한합니다. (`T extends U ? X : Y`)
```typescript
type U = string | number | boolean;

// type 식별자 = 타입 구현
type MyType<T> = T extends U ? string : never;

// interface 식별자 { 타입 구현 }
interface IUser<T> {
  name: string,
  age: T extends U ? number : never
}
```

```typescript
// `T`는 `boolean` 타입으로 제한.
interface IUser<T extends boolean> {
  name: string,
  age: T extends true ? string : number, // `T`의 타입이 `true`인 경우 `string` 반환, 아닌 경우 `number` 반환.
  isString: T
}

const str: IUser<true> = {
  name: 'Neo',
  age: '12', // String
  isString: true
}
const num: IUser<false> = {
  name: 'Lewis',
  age: 12, // Number
  isString: false
}
```

- 다음과 같이 삼항 연산자를 연속해서 사용할 수도 있습니다.
```typescript
type MyType<T> =
  T extends string ? 'Str' :
  T extends number ? 'Num' :
  T extends boolean ? 'Boo' :
  T extends undefined ? 'Und' :
  T extends null ? 'Nul' :
  'Obj';
```

### infer
- infer 키워드를 사용해 타입 변수의 타입 추론(Inference) 여부를 확인할 수 있습니다. 
- 기본 문법은 다음과 같습니다. (`T extends infer U ? X : Y`)
> U가 추론 가능한 타입이면 참, 아니면 거짓

```typescript
type MyType<T> = T extends infer R ? R : null;

const a: MyType<number> = 123;
```
- 여기서 타입 변수 R은 MyType<number>에서 받은 타입 number가 되고 infer 키워드를 통해 타입 추론이 가능한지 확인합니다.
- number 타입은 당연히 타입 추론이 가능하니 R을 반환하게 됩니다.(만약 R을 타입 추론할 수 없다면 null이 반환됩니다)
- 결과적으로 MyType<number>는 number를 반환하고 변수 a는 123을 할당할 수 있습니다.

- 이번에는 조금 더 복잡하지만 유용한 예제를 하나 살펴봅시다.
- ReturnType는 함수의 반환 값이 어떤 타입인지 반환합니다.
```typescript
type ReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer R ? R : any;

function fn(num: number) {
  return num.toString();
}

const a: ReturnType<typeof fn> = 'Hello';
```

- 위 예제에서 `typeof fn`은 (num: number) => string으로 반환 타입은 `string`입니다.
- 따라서 R은 string이고 역시 infer 키워드를 통해서 타입 추론이 가능하기 때문에 R을 반환합니다. 즉, string을 반환합니다.

### 함수
### this
- 함수를 다루는 데 있어 가장 중요한 내용 중 하나가 바로 `this`입니다.
- 함수 내 this는 전역 객체를 참조하거나(sloppy mode), undefined(strict mode)가 되는 등 우리가 원하는 `콘텍스트(context)`를 잃고 다른 값이 되는 경우들이 있습니다.
```typescript
const obj = {
  a: 'Hello~',
  b: function () {
    console.log(this.a); // obj.a
    // Inner function
    function b() {
      console.log(this.a); // global.a
    }
  }
};
```

- 특히 ‘호출하지 않는 메소드’를 사용하는 경우에 this로 인한 문제가 발생합니다.
- 우선, 다음 예제를 살펴봅시다.
- 객체 데이터 obj에서 b 메소드는 a 속성을 this를 통해 참조하고 있습니다.

```typescript
const obj = {
  a: 'Hello~',
  b: function () {
    console.log(this.a);
  }
};
```

- 위 객체를 기준으로 아래 예제와 같이 ‘호출하지 않는 메소드’를 사용(할당)하는 경우, this가 유효한 콘텍스트를 잃어버리고 a를 참조할 수 없게 됩니다.

```typescript
obj.b(); // Hello~

const b = obj.b;
b(); // Cannot read property 'a' of undefined

function someFn(cb: any) {
  cb();
}
someFn(obj.b); // Cannot read property 'a' of undefined

setTimeout(obj.b, 100); // undefined
```

- 이런 상황에서 this 콘텍스트가 정상적으로 유지되어 a 속성을 참조할 수 있는 방법을 알아봅시다.
- 첫 번째는 bind 메소드를 사용해 this를 직접 연결해 주는 방법입니다.

> 타입스크립트에서 bind, call, apply 메소드는 기본적으로 인수 타입 체크를 하지 않기 때문에, 
> 컴파일러 옵션에서 strict: true(혹은 strictBindCallApply: true)를 지정해 줘야 정상적으로 타입 체크를 하게 됩니다.

```typescript
obj.b(); // Hello~

const b = obj.b.bind(obj);
b(); // Hello~

function someFn(cb: any) {
  cb();
}
someFn(obj.b.bind(obj)); // Hello~

setTimeout(obj.b.bind(obj), 100); // Hello~
```

- 두 번째는 화살표 함수를 사용하는 방법입니다.
- 다음과 같이 화살표 함수를 이용해 유효한 콘텍스트를 유지하면서 메소드를 호출합니다.

> 화살표 함수는 호출된 곳이 아닌 함수가 생성된 곳에서 this를 캡처합니다.

```typescript
obj.b(); // Hello~

const b = () => obj.b();
b(); // Hello~

function someFn(cb: any) {
  cb();
}
someFn(() => obj.b()); // Hello~

setTimeout(() => obj.b(), 100); // Hello~
```

- 만약 클래스의 메소드 멤버를 정의하는 경우, 프로토타입(prototype) 메소드가 아닌 화살표 함수를 사용할 수 있습니다.

```typescript
class Cat {
  constructor(private name: string) {}
  getName = () => {
    console.log(this.name);
  }
}
const cat = new Cat('Lucy');
cat.getName(); // Lucy

const getName = cat.getName;
getName(); // Lucy

function someFn(cb: any) {
  cb();
}
someFn(cat.getName); // Lucy
```

- 여기서 주의할 점은 인스턴스를 생성할 때마다 개별적인 getName이 만들어지게 되는데, 
- 일반적인 메소드 호출에서의 화살표 함수 사용은 비효율적이지만 만약에 메소드를 주로 콜백으로 사용하는 경우엔 프로토타입의 새로운 클로져 호출보다 화살표 함수의 생성된 getName 참조가 훨씬 효율적일 수 있습니다.

### 명시적 this
- 다음 예제를 살펴보면, someFn 함수 내 this가 캡처할 수 있는 cat 객체를 call 메소드를 통해 전달 및 실행했지만, 엄격 모드에서 this는 암시적인(implicitly) any 타입이기 때문에 에러가 발생합니다.
> ‘엄격 모드’는 컴파일러 옵션에서 strict: true(혹은 noImplicitThis: true)인 경우를 말합니다.
```typescript
interface ICat {
  name: string
}

const cat: ICat = {
  name: 'Lucy'
};

function someFn(greeting: string) {
  console.log(`${greeting} ${this.name}`); // Error - TS2683: 'this' implicitly has type 'any' because it does not have a type annotation.
}
someFn.call(cat, 'Hello'); // Hello Lucy
```

- 이 경우 this의 타입을 명시적으로(explicitly) 선언할 수 있습니다.
- 다음과 같이 첫 번째 가짜(fake) 매개변수로 this를 선언합니다.

```typescript
interface ICat {
  name: string
}

const cat: ICat = {
  name: 'Lucy'
};

function someFn(this: ICat, greeting: string) {
  console.log(`${greeting} ${this.name}`); // ok
}
someFn.call(cat, 'Hello'); // Hello Lucy
```

### 오버로드(overloads)
- 타입스크립트의 ‘함수 오버로드(Overloads)’는 이름은 같지만 매개변수 타입과 반환 타입이 다른 여러 함수를 가질 수 있는 것을 말합니다.
- 함수 오버로드를 통해 다양한 구조의 함수를 생성하고 관리할 수 있습니다.
- 아래 예제에서 add 함수는 2개의 선언부와 1개의 구현부를 가지고 있습니다.
- 주의할 점은 함수 선언부와 구현부의 매개변수 개수가 같아야 합니다.
> 함수 구현부에 any가 자주 사용됩니다.
```typescript
function add(a: string, b: string): string; // 함수 선언
function add(a: number, b: number): number; // 함수 선언
function add(a: any, b: any): any { // 함수 구현
  return a + b;
}

add('hello ', 'world~');
add(1, 2);
add('hello ', 2); // Error - No overload matches this call.
```

- 인터페이스나 타입 별칭 등의 메소드 정의에서도 오버로드를 활용할 수 있습니다.
- 타입 단언이나 타입 가드를 통해 함수 선언부의 동적인 매개변수와 반환 값을 정의할 수 있습니다.

```typescript
interface IUser {
  name: string,
  age: number,
  getData(x: string): string[];
  getData(x: number): string;
}

let user: IUser = {
  name: 'Neo',
  age: 36,
  getData: (data: any) => {
    if (typeof data === 'string') {
      return data.split('');
    } else {
      return data.toString();
    }
  }
};

user.getData('Hello'); // ['h', 'e', 'l', 'l', 'o']
user.getData(123); // '123'
```

### 클래스
- 클래스의 생성자 메소드(constructor)와 일반 메소드(Methods) 멤버(Class member)와는 다르게, 
- 속성(Properties)은 `name: string;`와 같이 클래스 바디(Class body)에 별도로 타입을 선언합니다.
> 클래스 바디(Class body)는 중괄호 `{}`로 묶여 있는 영역을 의미합니다.
```typescript
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}
class Cat extends Animal {
  getName(): string {
    return `Cat name is ${this.name}.`;
  }
}
let cat: Cat;
cat = new Cat('Lucy');
console.log(cat.getName()); // Cat name is Lucy.
```

### 클래스 수식어(Modifiers)
- 타입스크립트와 관련된 클래스 수식어들을 살펴봅시다.
- 클래스 멤버(속성, 메소드)에서 사용할 수 있는 접근 제어자(Access Modifiers)들이 있습니다.
- 각 접근 제어자들의 차이점을 이해해 봅시다.
> 접근 제어자(Access Modifiers)는 클래스, 메서드 및 기타 멤버의 접근 가능성을 설정하는 객체 지향 언어의 키워드입니다.
```typescript
// public, protected, private로 선언된 것이 어떻게 접근이 가능한지에 대한 예
```

### 추상(Abstract) 클래스
- 추상(Abstract) 클래스는 다른 클래스가 파생될 수 있는 기본 클래스로, 인터페이스와 굉장히 유사합니다.
- abstract는 클래스뿐만 아니라 속성과 메소드에도 사용할 수 있습니다.
- 추상 클래스는 직접 인스턴스를 생성할 수 없기 때문에 파생된 후손 클래스에서 인스턴스를 생성해야 합니다.
```typescript
// Abstract Class
abstract class Animal {
  abstract name: string; // 파생된 클래스에서 구현해야 합니다.
  abstract getName(): string; // 파생된 클래스에서 구현해야 합니다.
}
class Cat extends Animal {
  constructor(public name: string) {
    super();
  }
  getName() {
    return this.name;
  }
}
new Animal(); // Error - TS2511: Cannot create an instance of an abstract class.
const cat = new Cat('Lucy');
console.log(cat.getName()); // Lucy

// Interface
interface IAnimal {
  name: string;
  getName(): string;
}
class Dog implements IAnimal {
  constructor(public name: string) {}
  getName() {
    return this.name;
  }
}
```

- 추상 클래스가 인터페이스와 다른 점은 속성이나 메소드 멤버에 대한 세부 구현이 가능하다는 점입니다.
```typescript
abstract class Animal {
  abstract name: string;
  abstract getName(): string;
  // Abstract class constructor can be made protected.
  protected constructor(public legs: string) {}
  getLegs() {
    return this.legs
  }
}
```

### Optional
- `?` 키워드를 사용하는 여러 선택적(Optional) 개념에 대해서 살펴봅시다.
###### 매개 변수
- 우선, 타입을 선언할 때 선택적 매개 변수(Optional Parameter)를 지정할 수 있습니다.
- 다음 예제를 보면 ? 키워드를 사용해 y를 선택적 매개 변수로 지정했습니다.
- 따라서 y가 받을 인수가 없어도 에러가 발생하지 않습니다.
```typescript
function add(x: number, y?: number): number {
  return x + (y || 0);
}
const sum = add(2);
console.log(sum);
```

- 위 예제는 정확히 다음 예제와 같습니다. 
- 즉, `?` 키워드 사용은 `| undefined`를 추가하는 것과 같습니다.

```typescript
function add(x: number, y: number | undefined): number {
  return x + (y || 0);
}
const sum = add(2, undefined);
console.log(sum);
```

###### 속성과 메서드
- `?` 키워드를 속성(Properties)과 메소드(Methods) 타입 선언에도 사용할 수 있습니다.
- 다음은 인터페이스 파트에서 살펴봤던 예제입니다.
- isAdult를 선택적 속성으로 선언하면서 더 이상 에러가 발생하지 않습니다.
```typescript
interface IUser {
  name: string,
  age: number,
  isAdult?: boolean
}

let user1: IUser = {
  name: 'Neo',
  age: 123,
  isAdult: true
};

let user2: IUser = {
  name: 'Evan',
  age: 456
};
```

- Type이나 Class에서도 사용할 수 있습니다.
```typescript
interface IUser {
  name: string,
  age: number,
  isAdult?: boolean,
  validate?(): boolean
}
type TUser = {
  name: string,
  age: number,
  isAdult?: boolean,
  validate?(): boolean
}
abstract class CUser {
  abstract name: string;
  abstract age: number;
  abstract isAdult?: boolean;
  abstract validate?(): boolean;
}
```

###### 체이닝(chaining)
- 다음 예제는 str 속성이 undefined일 경우 toString 메소드를 사용할 수 없기 때문에 에러가 발생합니다.
- str 속성이 문자열이라는 것을 단언하면 문제를 해결할 수 있지만, 더 간단하게 선택적 체이닝(Optional Chaining) 연산자 ?.를 사용할 수 있습니다.
```typescript
obj?.prop;
obj?.[expr];
arr?.[index];
func?.(args);
```

```typescript
// Error - TS2532: Object is possibly 'undefined'.
function toString(str: string | undefined) {
  return str.toString();
}

// Type Assertion
function toString(str: string | undefined) {
  return (str as string).toString();
}

// Optional Chaining
function toString(str: string | undefined) {
  return str?.toString();
}
```

- 특히 && 연산자를 사용해 각 속성을 Nullish 체크(null이나 undefined를 확인)하는 부분에서 유용
```typescript
// Before
if (foo && foo.bar && foo.bar.baz) {}

// After-ish
if (foo?.bar?.baz) {}
```

###### nullish 병합 연산자
- 일반적으로 논리 연산자 `||`를 사용해 Falsy 체크(`0`, `""`, `NaN`, `null`, `undefined`를 확인)하는 경우가 많습니다.
- 여기서 0이나 "" 값을 유효 값으로 사용하는 경우 원치 않는 결과가 발생할 수 있는데, 이럴 때 유용한 Nullish 병합(Nullish Coalescing) 연산자 `??`를 타입스크립트에서 사용할 수 있습니다.
```typescript
const foo = null ?? 'Hello nullish.';
console.log(foo); // Hello nullish.

const bar = false ?? true;
console.log(bar); // false

const baz = 0 ?? 12;
console.log(baz); // 0
```

### 모듈
### 내보내기(export)와 가져오기(import)
### 모듈의 타입선언
### typeRoots와 types 옵션

### TS 유틸리티 타입
### Partial
### Required
### Readonly
### Record
### Pick
### Omit
### Exclude
### Extract
### NonNullable
### Parameters





