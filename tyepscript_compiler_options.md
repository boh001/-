# 타입스크립트 컴파일러가 타입 선언을 참조하는 과정

타입스크립트 컴파일러가 컴파일러 옵션에 따라서 타입 선언 파일을 참조하는 과정에 대하여

## 타입스크립트 컴파일러란?
타입스크립트를 특정 타켓 버전의 자바스크립트로 컴파일 해주는 컴파일러입니다.

작동 순서
- 타입스크립트로 작성된 소스코드를 AST로 변환
- 타입체커가 AST를 확인
- AST를 자바스크립트 소스코드로 변환

타입체커에서 타입 오류가 발생해도 컴파일된 결과물은 출력됩니다.

## 타입 선언 파일(.d.ts)이란?
자바스크립트로 작성된 모듈을 사용하려면 컴파일러가 타입 검증을 할 수 없습니다.
컴파일러에게 모듈의 타입을 알려주기 위해서 타입 선언 파일이 필요하다. 

### declare 키워드
컴파일러에게 해당 변수나 함수가 이미 존재한다는 것을 알리는 역할을 합니다.
컴파일러는 코드의 정적 타입 확인을 위해 사용할 뿐 자바스크립트로 컴파일하지 않습니다.
```javascript
// moduleA
export const object1 = {
  name: "camel",
  age: 28
}
export const object2 = {
  name: "camel",
  age: 28
}
```
```typescript
// moduleA.d.ts
export declare let object2: { name: string, age: number }

// index.ts
import { object1, object2 } from "moduleA"

object2.name = "kim sang hyeon"

// Error: property 'name' does not exist
object1.name = "kim sang hyeon"
```
## 타입스크립트 모듈 탐색 방식
```typescript
import modulename from './modulename'; // relative module import
import modulename from 'modulename'; // non-relative module import
```
- 상대경로 모듈 불러오기
- 비 상대경로 모듈 불러오기
## 컴파일러 옵션