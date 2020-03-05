---
layout: post
title:  "Out of bounds"
date:   2020-02-22 23:17:00 
categories: Array

---

Dictionary는 '키' 값이 유효하지 않을 경우에 nil을 반환하지만, 

<br>

Array의 경우에는 **Out of bounds**와 함께 app crash가 발생한다.

array를 안전하게 사용하기 위해서 아래 코드처럼 사용할 수 있다.

<br>

```swift
extension Array {
    subscript(safe index: Int) -> Element? {
        return indices ~= index ? self[index] : nil
    }
}
```

<br><br>

### ~= 연산자

패턴을 비교하는 연산자이다. 

``` swift
static func ~= (pattern: Range<Array<Element>.Index>, value: Int) -> Bool
```

~= 을 사용하지 않았다면 아래 코드와 같이 표현해야되지만 ~=을 사용해서 깔끔하게 표현했다.

```swift
if index >= 0 && index < endIndex { }
```







<br>

<br>

Reference

---

[민소네](http://minsone.github.io/programming/check-index-of-array-in-swift)

