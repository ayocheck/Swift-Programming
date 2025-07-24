## Part 4. 확장

### Chapter 17. 서브스크립트

- `subscript`
    - 여러 매개변수를 가질 수 있다.
    - 매개변수 기본값을 가질 수 있다.
    - `inout` 매개변수는 가질 수 없다.
    - 하나의 타입이 여러 서브스크립트를 가질 수 있다.
    - 코드 예시
        
        ```swift
        struct Student {
            var name: String
            var number: Int
        }
        
        class School {
            var number = 0
            var students: [Student] = []
            
            func addStudent(name: String) {
                let student = Student(name: name, number: number)
                students.append(student)
                number += 1
            }
            
            subscript(index: Int = 0) -> Student? {
                if index < number {
                    return students[index]
                }
                
                return nil
            }
        }
        
        let school = School()
        school.addStudent(name: "bello")
        school[0]?.name // "bello"
        ```
        
    - 코드 응용
        
        ```swift
        extension Array {
            // 안전한 인덱스 접근
            subscript(safe index: Int) -> Element? {
                return indices.contains(index) ? self[index] : nil
            }
        }
        
        let numbers = [1, 2, 3, 4, 5]
        print("안전한 접근 numbers[10]: \(numbers[safe: 10] ?? -1)")
        ```
        
### Chapter 18. 상속

- 부모, 자식, 기반(상속을 받지 않는) 클래스
- `override`
    - `super`
- `final`
- `convenience init`
    - 지정 생성자와의 관계
        1. 자식 클래스의 지정 생성자는 부모 클래스의 지정 생성자를 반드시 호출해야 한다.
        2. 편의 생성자는 자신을 정의한 클래스의 다른 생성자를 반드시 호출해야 한다.
        3. 편의 생성자는 궁극적으로 지정 생성자를 반드시 호출해야 한다.
- 클래스의 2단계 초기화
    - 1단계: 클래스에 정의한 저장 프로퍼티에 초깃값 할당
    - 2단계: 저장 프로퍼티들을 사용자 정의할 기회
- 생성자 자동 상속
    - 자식 클래스에서 프로퍼티 기본값을 모두 제공한다고 할 때, 다음의 2가지 규칙을 따른다면 생성자가 자동으로 상속된다.
        1. 자식 클래스에서 별도의 지정 생성자를 구현하지 않는다면, 부모 클래스의 지정 생성자가 자동으로 상속된다.
        2. 규칙 1.에 따라 자식 클래스에서 부모 클래스의 지정 생성자를 자동으로 상속받은 경우, 또는 부모 클래스의 지정 생성자를 모두 재정의하여 부모 클래스와 동일한 지정 생성자를 모두 사용할 수 있는 상황이라면, 부모 클래스의 편의 생성자가 모두 자동으로 상속된다.
- `required init`
    - `required`를 생성자 앞에 명시한다면 상속받는 자식 클래스에서 반드시 해당 생성자를 구현해야 한다.

### Chapter 19. 타입캐스팅

- 스위프트의 타입캐스팅
    - 인스턴스의 타입을 확인
    - 자신을 다른 타입의 인스턴스인 것처럼 행세
- 타입 확인 연산자 `is`
    - 어떤 클래스의 인스턴스인지 확인
    - 다른 방법으로는 `type(of:)`와 메타타입을 비교
- 다운캐스팅
    - 부모 타입을 자식 타입으로 캐스팅
- 타입캐스팅 연산자 `as?`, `as!`
    - 항상 성공하는 경우는 `as`도 사용 가능
        - 컴파일러가 판단
- `Any`, `AnyObject`
    - `Any`
        - 함수 타입을 포함한 모든 타입
    - `AnyObject`
        - 클래스 타입

### Chapter 20. 프로토콜

- 스위프트는 **프로토콜 지향 프로그래밍(POP)**
- 프로토콜 `protocol`
    - 특정 역할을 하기 위한 메서드, 프로퍼티, 기타 요구사항 등의 청사진
- 프로토콜의 생성자 요구
    - **상속이 가능한** 클래스의 경우 프로토콜의 생성자를 구현할 때, `required`를 반드시 명시해야 한다.
- 클래스 전용 프로토콜
    - 프로토콜 상속에 `AnyObject`를 추가하면 된다.
- 프로토콜의 선택적 요구
    - `@objc optional protocol`
    - objc 속성이 반드시 필요 → Objective-C 클래스를 상속한 클래스에서만 채택이 가능하다는 뜻
        - ex) `NSObject`
- 실존 타입
    - 프로토콜을 타입으로 활용할 때 이를 실존 타입이라 한다.
    - 실존 타입으로 활용될 때는 구체 타입과 구분하기 위해 **`any`를 붙여준다.**
    - 실존 타입을 사용하면 실행 시점에 확인해야 하기 때문에 컴파일 성능 최적화가 어렵다.
- 위임
    - 자신의 책임을 다른 타입의 인스턴스에게 위임하는 디자인 패턴

### Chapter 21. 익스텐션

- **타입에 새로운 기능을 추가할 수는 있지만, 기존에 존재하는 기능을 재정의할 수는 없다.**
    - 연산 타입 프로퍼티, 연산 프로퍼티
    - 타입 메서드, 메서드
    - 생성자
    - 서브스크립트
    - 중첩 타입
    - 특정 프로토콜을 준수할 수 있도록 기능 추가
- 상속과 비교
    
    
    | 구분 | 상속 | 확장 |
    | --- | --- | --- |
    | 확장 | 수직 확장  | 수평 확장 |
    | 사용 | 클래스 타입에서만 사용 | 클래스, 구조체, 프로토콜, 제네릭 등 모든 타입에서 사용 |
    | 재정의 | 재정의 가능 | 재정의 불가 |