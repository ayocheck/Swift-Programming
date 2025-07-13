## Part 1. 스위프트 기초

### Chapter 1. 스위프트

- Swift의 특성
    - Safe, Fast, Expressive
- Swift가 차용하는 패러다임
    - 명령형, 객체지향, 함수형, 프로토콜

### Chapter 2. 스위프트 시작하기

- 명명 규칙을 위한 가이드라인
    - Swift API Design Guideline, Coding Guidelines for Cocoa
- 콘솔로그
    - `print`, `dump`
- `“\()”`
    - CustomStringConvertible과 `description`
- `var`, `let`

### Chapter 3. 데이터 타입 기본

- 스위프트의 데이터 타입은 **Struct**를 기반으로 구현되어 있다.
- Int, UInt
- Bool
- Float, Double
- Character
- String
    - 특수문자
        - `\n`: 줄바꿈
        - `\\`: 백슬래시
        - `\”`: 큰따옴표
        - `\t`: 탭
        - `\0`: null
- Any, AnyObject, `nil`

### Chapter 4. 데이터 타입 고급

- 데이터 타입 안심, 타입 추론
- 타입 별칭
- 튜플
- 컬렉션
    - 배열, 딕셔너리, 세트
- 열거형
    - 원시 값, `rawValue`
    - 연관 값
    - CaseIterable와 `allCases`
    - 순환 열거형, `indirect`
    - 비교 가능한 열거형, Comparable

### Chapter 5. 연산자

- 할당
- 산술
- 비교
- 삼항 조건
- 범위
- 부울
- 비트
- 복합 할당
- 오버플로

### Chapter 6. 흐름 제어

- 조건문
    - `if`
        - `else if`, `else`
        - if 표현문을 이용한 변수 할당
            
            ```swift
            let someInt: Int = 100
            
            let size: String = if someInt > 10 { "큰 수" } else { "작은 수" }
            ```
            
    - `switch`
        - `case`, `default`, `@unknown`
        - `break`, `fallthrough`
        - switch 표현문을 이용한 변수 할당
            
            ```swift
            enum Menu {
                case chicken, pizza, hamburger
            }
            
            let lunchMenu: Menu = .pizza
            
            let menu: String = switch lunchMenu {
            case .chicken: "치킨"
            case .pizza: "피자"
            case .hamburger: "햄버거"
            }
            ```
            
- 반복문
    - `for-in`, `while`, `repeat-while`
        - `break`, `continue`

### Chapter 7. 함수

- 스위프트에서 함수는 일급객체
    - 값으로 사용 가능
- 오버라이드, 오버로드
- `@discardableResult`
    - 함수의 반환 값을 무시

### Chapter 8. 옵셔널

- 옵셔널은 열거형
    - `none`, `some`
- 강제 추출, 옵셔널 바인딩, 암시적 추출 옵셔널
