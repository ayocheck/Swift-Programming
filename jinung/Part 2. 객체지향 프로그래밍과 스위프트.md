## Part 2. 객체지향 프로그래밍과 스위프트

### Chapter 9. 구조체와 클래스

- `struct`
    - 값 타입
        - **전달될 값이 복사**되어 전달
    - 멤버와이즈 이니셜라이저
- `class`
    - 참조 타입
        - **참조(메모리 주소)**가 전달
    - 클래스의 인스턴스 ⇒ **객체**
    - 식별 연산자 `===`

<aside>
💡

애플에서 권장하는 구조체를 선택하는 기준

- 연관된 간단한 값의 집합을 캡슐화하는 것만이 목적일 때
- 캡슐화한 값을 참조하는 것보다 복사하는 것이 합당할 때
- 구조체에 저장된 프로퍼티가 값 타입이며, 참조하는 것보다 복사하는 것이 합당할 때
- 다른 타입으로부터 상속받거나 자신을 상속할 필요가 없을 때
</aside>

- 스위프트의 복사처리
    - 스위프트는 꼭 필요한 경우에만 ‘진짜 복사’

### Chapter 10. 프로퍼티와 메서드

- 프로퍼티
    - 저장
    - 지연 저장 `lazy`
    - 연산
        - `get`
        - `set`, `newValue`
    - 프로퍼티 감시자
        - `willSet`, `newValue`
        - `didSet`, `oldValue`
    - 타입
        - 타입 저장 프로퍼티는 (다중 스레드 환경이라고 하더라도 단 한번만) 지연 연산된다.
    - 키 경로
- 메서드
    - 인스턴스 메서드
        - 값 타입에 한해서만 `mutating`
        - `self` = 인스턴스
        - `callAsFunction`
            - 인스턴스를 함수처럼 호출하도록 하는 메서드
                
                ```swift
                struct Calculator {
                    func callAsFunction(_ a: Double, _ b: Double, operation: String) -> Double {
                        switch operation {
                        case "+": return a + b
                        case "-": return a - b
                        case "*": return a * b
                        case "/": return b != 0 ? a / b : 0
                        default: return 0
                        }
                    }
                }
                
                let calc = Calculator()
                let sum = calc(10, 5, operation: "+") // 15
                let product = calc(10, 5, operation: "*") // 50
                print("Sum: \(sum), Product: \(product)")
                ```
                
    - 타입 메서드
        - `static`: 상속 후 재정의 불가능
        - `class`: 상속 후 재정의 가능
        - `self` = 타입 그 자체

### Chapter 11. 인스턴스 생성 및 소멸

- `init`, `init?`
- `deinit`
    - 클래스의 인스턴스에서만 구현 가능
    - 디스크의 파일을 불러와 사용할 떄, 변경 사항을 저장하고 닫아줘야 메모리에서 해제된다 → `deinit`에서 실행

### Chapter 12. 접근제어

- OOP의 캡슐화, 은닉화와 연관
- 스위프트의 접근수준
    
    
    | 접근수준 | 키워드 | 범위 | 비고 |
    | --- | --- | --- | --- |
    | 개방 접근수준 | `open` | 모듈 외부까지 | 클래스에서만 사용 |
    | 공개 접근수준 | `public` | 모듈 외부까지 |  |
    | 패키지 접근수준 | `package` | 패키지 내부 |  |
    | 내부 접근수준 | `internal` | 모듈 내부 |  |
    | 파일 외부 비공개 접근수준 | `fileprivate` | 파일 내부 |  |
    | 비공개 접근수준 | `private` | 기능 정의 내부 |  |