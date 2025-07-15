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