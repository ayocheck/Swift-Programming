## Part 5. 스위프트 고급

### Chapter 24. 타입 중첩

- 특정 클래스나 구조체와 연관된 기능을 하는 열거형을 외부에 노출할 필요가 없을 때, 해당 클래스/구조체 내부에 선언하여 역할을 명확히 한정할 수 있다.
    - 타입을 다른 타입 내부에 중첩하여 타입의 목적성을 명확히 할 수 있다.

### Chapter 25. 패턴

- 패턴
    - 단독 또는 복합 값의 구조를 나타내는 것
- 패턴 매칭
    - 코드에서 어떤 패턴의 형태를 찾아내는 행위
- 스위프트의 패턴들
    - **값을 해제(추출)하거나 무시하는 패턴**
        - 와일드카드, 식별자, 값 바인딩, 튜플
    - **패턴 매칭을 위한 패턴**
        - 열거형 케이스, 옵셔널, 표현, 타입캐스팅
- 값 바인딩 패턴
    - 변수 또는 상수의 이름에 매치된 값을 바인딩하는 패턴
    - 코드 예시
        
        ```swift
        import Foundation
        
        let bello = ("bello", 27, "Male")
        
        switch bello {
        case let (name, age, gender):
            print("Name: \(name), Age: \(age), Gender: \(gender)")
        }
        
        switch bello {
        case (let name, let age, let gender):
            print("Name: \(name), Age: \(age), Gender: \(gender)")
        }
        ```
        
- 열거형 케이스 패턴
    - 값을 열거형의 `case`와 매치시킨다.
    - `if case`, `guard case`, `while case`, `case let`
- 옵셔널 패턴
    - 코드 예시
        
        ```swift
        import Foundation
        
        var optionalValue: Int? = 100
        
        if case .some(let value) = optionalValue {
            print(value)
        }
        
        if case let value? = optionalValue {
            print(value)
        }
        
        func isItHasValue(_ optionalValue: Int?) {
            guard case .some(let value) = optionalValue else {
                print("none")
                return
            }
            print(value)
        }
        
        while case .some(let value) = optionalValue {
            print(value)
            optionalValue = nil
        }
        
        let arrayOfOptionalInts: [Int?] = [nil, 2, 3, nil, 5]
        
        for case let number? in arrayOfOptionalInts {
            print(number)
        }
        ```
        
- 타입캐스팅 패턴
    - `is` 패턴
        - `switch`의 `case`에서만 사용 가능
    - `as` 패턴
    - 코드 예시
        
        ```swift
        import Foundation
        
        let someValue: Any = 100
        
        switch someValue {
        case is String:
            print("It's String.")
        case let value as Int:
            print("It's Integer.")
        default:
            print("String도 Int도 아닙니다.")
        }
        ```
        
- 표현 패턴
    - `switch`의 `case`에서만 사용 가능
    - `~=`를 활용
        - 중복 정의
        - 직접 구현
