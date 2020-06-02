---
layout: post
title: "Publisher"
excerpt: ""
categories: [Combine]
comments: true
---

## Publisher 

publisher는 하나 이상의 subscibers에게 시간이 지남에 따라 값을 방출할 수 있다.

publisher는 receive(subscriber:)를 통해서 subscriber를 받는다.

- receive(subscription:) 구독 요청을 알고 Subscription을 리턴한다. 구독자는 구독권을 사용해서  publisher로 부터 값을 요구한다.
- receive(_ :) 값을 전달한다.
- receive(completion:) publishing이 끝나거나 error가 발생했다고 알린다.



0개 이상의  output을 가질 수 있으며, 성공, 실패하면 더 이상 이벤트가 발생하지 않는다.



### Publisher Protocol

```swift
public protocol Publisher {
 	associatedtype Output
 	associatedtype Failure : Error
  // 1
 	func receive<S>(subscriber: S)
 		where S: Subscriber,
 		Self.Failure == S.Failure,
 		Self.Output == S.Input
 }
 
 extension Publisher {
	// 2
 	public func subscribe<S>(_ subscriber: S)
 		where S : Subscriber,
 		Self.Failure == S.Failure,
 		Self.Output == S.Input
 }
```

- 1: subscriber가 구독이 되어있는 상태에서 값 
- subscriber의 Input, Failure 와 publisher의 Output, Failure의 타입은 일치해야한다.
- 2: subscriber를 받아서 subscription을 생성한다.

<img width="523" alt="Screen Shot 2020-05-25 at 11 58 30" src="https://user-images.githubusercontent.com/48466830/82774375-9ff6ac80-9e7f-11ea-87ac-9b96f35ebd58.png">