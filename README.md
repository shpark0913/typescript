## TypeScript 학습 내용을 정리한 레포지토리입니다.

---





## TypeScript

## = JavaScript + Type 문법

---

## 왜 사용할까?

1. 타입
   - JavaScript는 Dynamic Typing 가능
     - 코드 길게 짤 땐 자유도&유연성은 나쁜 요인
   - TypeScript는 타입 엄격히 검사함
2. Error Message 퀄리티가 JavaScript에 비해 자세함
   - TyperScript를 언어보다는 코드 에디터 부가기능 역할로 봐도 무방

---

## React PJT에서 Typescript 사용할 경우

1. 이미 있는 React PJT에 설치하는 경우
   
   ```jsx
   npm install --save typescript @types/node @types/react @types/react-dom @types/jest
   ```
   
   - 이제 .js 파일을 .ts 파일로 바꿔서 이용가능

2. React PJT 새로 만드는 경우
   
   ```jsx
   npx create-react-app my-app --template typescript
   ```

---

## 컴파일

브라우저는 .ts 파일 읽지 못함

⇒ 따라서 .js 파일로 변환해야 함

⇒ 터미널 켜서 `tsc -w` 입력해두면 자동 변환됨

- 이 변환되는 과정을 `컴파일` 이라고 함
  - 컴파일 옵션을 `tsconfig.json` 에 설정함

[tsconfig](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/322f0124-40a1-4a21-970b-0014e5b02d5a/Untitled.json)

---

## 간단한 변수 타입 지정 가능

- `let 이름 :string = 'kim'`
  
  - `이름`이라는 변수엔 string type만 들어올 수 있음

- 변수 타입
  
  - string, number, boolean, null, undefined, bigint, [ ], { } 등

- `let 이름 :[] = ['kim', 'park']`
  
  - 하지만 array 안 물품들의 타입 지정해야 함
  - array 타입 지정
    - `let 이름 :string[] = ['kim', 'park']`
      - `이름`변수에는 string이 담긴 array만 들어올 수 있음
  - object 타입 지정
    - `let 이름 :{ name : string } = { name : ‘kim’ }`
      - `let 이름 :{ name? : string } = { name : ‘kim’ }`
        - 이렇게 하면 name 속성이 옵션이라는 뜻

- 다양한 타입이 들어올 수 있게 하려면 Union type
  
  - `let 이름 :string | number = 'kim'`
    - `이름` 변수에는 string 혹은 number가 들어옴
  - `let 이름 :string[] | number = 123`
    - `이름` 변수에는 string이 담긴 array나 number 들어옴

- 타입은 변수에 담아서 사용 가능 : `Type alias`
  
  ```jsx
  type Name = string | number
  
  let 이름 :Name = 123
  ```
  
  - 타입명은 대문자로 보통 작명함
    - 일반 변수와 차별화해서 관리

- `literal type`
  
  ```jsx
  type NameType = 'kim' | 'park'
  let 이름 :NameType = 'kim'
  ```
  
  - `이름` 이라는 변수에 ‘kim’ 또는 ‘park’ 만 들어올 수 있음

- 함수 만들 때도 타입 지정 가능
  
  ```jsx
  function 함수(x :number) :number {
      return x * 2
  }
  ```
  
  - 위 함수는 파라미터로 number, return 값으로 number

- array에 쓸 수 있는 tuple 타입
  
  ```jsx
  // 무조건 1st는 number, 2nd는 boolean
  
  type Member = [number, boolean]
  let john :Member = [123, true]
  ```

- object에 타입 지정해야 할 속성이 너무 많은 경우
  
  ```jsx
  type Member = {
      name : string
  }
  
  let john :Member = { name : 'kim' }
  ```
  
  - john이라는 변수는 {name : string} 이런 변수만 가능
  
  - 만약 name 뿐 아니라, age 등등 매우 많은 속성들이 들어간다면?
    
    ```jsx
    type Member = {
        [key : string] : string
    }
    
    // [key : string] => 모든 object 속성
    // [key : string] : string => 글자로 된 모든 object 속성의 타입은 :string
    ```
