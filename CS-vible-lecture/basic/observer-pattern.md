# 옵저버 패턴

> 주체가 어떤 객체 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 디자인 패턴이다.

```swift
class Dog {
    var name: String = "강아지" {
        didSet {
            print("\(oldValue)")
        }
        willSet {
            print("\(newValue)")
        }
    }
}
```

위와 같이 값이 바뀌는 시점을 알려줄 수 있다.
