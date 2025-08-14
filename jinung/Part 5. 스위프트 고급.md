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

### Chapter 26. where 절

- `where`절 용도
    - 패턴과 결합하여 조건 추가
    - 타입에 대한 제약 추가

### Chapter 27. ARC

- 스위프트는 메모리 관리를 위해 ARC를 사용
    - Automatic Reference Counting 자동 참조 카운팅
    - 개발자가 메모리 관리에 신경을 덜 수 있도록 하기 위함.
- 자바의 가비지 컬렉션과의 차이
    
    
    | 메모리 관리 기법 | ARC | 가비지 컬렉션 |
    | --- | --- | --- |
    | 참조 카운팅 시점 | 컴파일 시 | 프로그램 동작 중 |
    | 장점 | - 컴파일 당시 이미 인스턴스의 해제 시점이 정해져 있어서 인스턴스가 언제 메모리에서 해제될지 예측할 수 있다.
    - 컴파일 당시 이미 인스턴스의 해제 시점이 정해져 있어서 메모리 관리를 위한 시스템 자원을 추가할 필요가 없다. | - 상호 참조 상황 등의 복잡한 상황에서도 인스턴스를 해제할 수 있는 가능성이 더 높다.
    - 특별히 규칙에 신경 쓸 필요가 없다. |
    | 단점 | - ARC의 작동 규칙을 모르고 사용하면 인스턴스가 메모리에서 영원히 해제되지 않을 가능성이 있다. | - 프로그램 동작 외에 메모리 감시를 위한 추가 자원이 필요하므로 한정적인 자원 환경에서는 성능 저하가 발생할 수 있다.
    - 명확한 규칙이 없기 때문에 인스턴스가 정확히 언제 메모리에서 해제될지 예측하기 어렵다. |
- 강한참조
    - 강한참조 순환
        - 두 인스턴스가 서로를 참조하는 상황에서 강한참조 순환이 발생할 수 있다.
        - 강한참조 순환은 메모리 누수로 이어진다.
        - 코드 예시
            
            ```swift
            import Foundation
            
            class Person {
                var room: Room?
                
                let name: String
                
                init(name: String) {
                    self.name = name
                }
                
                deinit {
                    print("\(name) is being deinitialized")
                }
            }
            
            class Room {
                var host: Person?
                
                let number: String
                
                init(number: String) {
                    self.number = number
                }
                
                deinit {
                    print("Room \(number) is being deinitialized")
                }
            }
            
            var yagom: Person? = Person(name: "yagom")      // Person 인스턴스의 참조 횟수 : 1
            var room: Room? = Room(number: "505")      // Room 인스턴스의 참조 횟수 : 1
            
            room?.host = yagom // Person 인스턴스의 참조 횟수 : 2
            yagom?.room = room // Room 인스턴스의 참조 횟수 : 2
            
            yagom = nil // Person 인스턴스의 참조 횟수 : 1
            room = nil // Room 인스턴스의 참조 횟수 : 1
            
            // Person 인스턴스를 참조할 방법 상실 - 메모리에 잔존
            // Room 인스턴스를 참조할 방법 상실 - 메모리에 잔존
            ```
            
- 약한 참조
    - 자신이 참조하는 인스턴스의 참조 횟수를 증가시키지 않는다.
    - `weak`
    
    <aside>
    💡
    
    약한참조와 상수, 옵셔널
    
    약한참조는 상수에 쓰일 수 없다. 자신이 참조하던 인스턴스가 메모리에서 해제된다면 `nil`이 할당될 수 있어야 하기 때문이다. 그래서 약한참조를 할 떄는 값을 변경할 수 있는 변수로 선언해야 한다. 더불어 `nil`이 할당될 수 있어야 하므로 약한참조는 항상 옵셔널이어야 한다.
    
    </aside>
    
- 미소유참조
    - 약한참조와 다르게 자신이 참조하는 인스턴스가 항상 메모리에 존재할 것이라는 전제를 기반으로 동작한다.
        - 참조하는 인스턴스가 메모리에서 해제되더라도 `nil`을 할당하지 않는다.
        - 미소유참조를 하면서 메모리에서 해제된 인스턴스에 접근하려 한다면 런타임 오류가 발생한다.
    - `unowned`
- 미소유 옵셔널 참조
    - 클래스를 참조하는 옵셔널을 `unowned`로 표시할 수 있다.
        - 미소유 옵셔널 참조와 약한참조를 같은 상황에 사용할 수 있다.
    - 미소유 옵셔널 참조는 `nil`이 될 수 있다.
        - 하지만 약한참조처럼 자동으로 할당하지 않고, 개발자가 직접 할당해 주어야 한다.
- 미소유참조와 암시적 추출 옵셔널 프로퍼티
    - 암시적 추출 옵셔널 프로퍼티는 생성자의 2단계 초기화 조건을 충족시키기 위해 사용할 수 있다.
    - 미소유참조 프로퍼티는 강한참조를 피하면서도 상수로 지정하기 위해 사용할 수 있다.
        - 단, 참조 대상이 절대 `nil`이 되지 않는다고 보장되어야 한다.
    - 코드 예시
        
        ```swift
        import Foundation
        
        class Company {
            let name: String
            
            var ceo: CEO!
            
            init(name: String, ceoName: String) {
                self.name = name
                self.ceo = CEO(name: ceoName, company: self)
            }
            
            func introduce() {
                print("\(name)의 CEO는 \(ceo.name)입니다.")
            }
        }
        class CEO {
            let name: String
            
            unowned let company: Company
            
            init(name: String, company: Company) {
                self.name = name
                self.company = company
            }
            
            func introduce() {
                print("\(name)는 \(company.name)의 CEO입니다.")
            }
        }
        
        let company: Company = Company(name: "무한상사", ceoName: "김태호")
        company.introduce()
        company.ceo.introduce()
        ```
        
- 클로저의 강한참조 순환
    - 클로저의 강한참조 순환 문제
        - 클로저 내부에서 `self`를 접근할 때 클로저의 값 획득 특성으로 인해 강한참조 순환이 발생한다.
    - 캡처리스트
        - `[]`, `in`
        - 캡처리스트에 명시된 요소가 참조 타입이 아니라면, 해당 요소들은 클로저가 생성될 때 초기화된다.
            - 값 타입과 캡처리스트 코드 예시
                
                ```swift
                import Foundation
                
                var a = 0, b = 0
                let closure = { [a] in // a라는 값을 강한캡처, 변수 a와 별개
                    print(a, b)
                    b = 20 // b를 강한참조
                }
                
                a = 10
                b = 10
                closure() // 0 10
                print(b) // 20
                ```
                
            - 참조 타입과 캡처리스트 코드 예시
                
                ```swift
                import Foundation
                
                class SimpleClass {
                    var value: Int = 0
                }
                
                var x = SimpleClass(), y = SimpleClass()
                
                let closure = { [x] in // 클래스 x를 강한캡처
                    print(x.value, y.value)
                }
                
                x.value = 10
                y.value = 10
                
                closure() // 10 10
                ```
                
        - `weak`, `unowned`

### Chapter 28. 오류처리

- 오류처리
    - 프로그램이 오류를 일으켰을 때 이것을 감지하고 회복시키는 과정
- `Error`
    - 사실상 요구사항이 없는 빈 프로토콜
- `throw`
- 스위프트에서 오류를 처리하기 위한 방법
    - 함수에서 발생한 오류를 해당 함수를 호출한 코드에 알리는 방법
        - `try`, `try?`, `try!`로 던져진 오류를 받을 수 있다.
        - 함수, 메서드, 생성자 뒤에 `throws`를 사용하여 오류를 던질 수 있다.
    - `do-catch` 구문을 이용하여 오류를 처리하는 방법
    - 옵셔널 값으로 오류를 처리하는 방법
        - `try?`를 사용하여 에러 발생 시, `nil`로 대체할 수 있다.
    - 오류가 발생하지 않을 것이라고 확신하는 방법
        - 오류가 발생하지 않을 거라고 확신하는 상황이라면, `try!`를 사용할 수 있다.
        - 오류가 발생하면 런타임 오류가 발생한다.
    - `rethrows`
        - 함수나 메서드는 자신의 매개변수로 전달받은 함수가 오류를 던진다는 것을 `rethrows`를 통해 나타낼 수 있다.
    - `defer`
        - 현재 코드 범위를 벗어나기 전까지 실행을 미루고 있다가 프로그램 실행 흐름이 코드 범위를 벗어나기 직전 실행된다.
- 오류 타입 지정
    - 어떤 타입의 오류를 던지고 받을지 명확히 명시하고 싶을 때
    - 코드 예시
        
        ```swift
        import Foundation
        
        enum PhoneCallError: Error {
            case noSignal
            case outOfBattery
            case airplaneMode
        }
        
        enum TextMessageError: Error {
            case wrongNumber
            case blocked
        }
        
        func makePhoneCall() throws(PhoneCallError) { // throw TextMessageError.wrongNumber
            // 오류 발생!!
            throw PhoneCallError.noSignal
        }
        
        do {
            try makePhoneCall()
        } catch .noSignal {
            print("통신 연결 상태가 좋지 않습니다")
        } catch .outOfBattery {
            print("배터리가 부족합니다")
        } catch .airplaneMode {
            print("비행기 모드 상태입니다")
        }
        ```
