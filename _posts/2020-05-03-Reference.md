---
layout: post
title:  "Reference"
date:   2020-05-03 23:12:00 
categories: iOS

---

문득 stroyboard에 객체를 IBOutlet으로 연결하면 기본적으로 weak로 선언되었고, weak를 지우고 strong으로 선언해도 차이가 보이지 않았다. class를 사용을 지양하라는 말만 읽었었고, reference count를 0으로 만들지않으면 memory lick이 발생한다고 읽었었다. 그래서 코드로 view객체를 생성할때 기본적으로 strong이 아닌 weak로 변경해야 겠다는 생가이 들어서 weak로 변경했다.

<!--more-->

``` swift
    private weak var label: UILabel! = {
        let label = UILabel()
        label.textAlignment = .center
        label.font = UIFont.boldSystemFont(ofSize: UIFont.boldTitleSize)
        return label
    }()

```

프로젝트를 런했을때 오류가 발생했었고 그 이유는 label이 해제(nil) 되었다. 스토리 보드에서 IBOutlet으로 연결 했을때는 weak와 strong 둘다 사용 가능했지만, 코드로 생성했을 때는 weak로 선언하면 에러가 발생하는 이유가 궁금했다.

delegate pattern을  다시 생각해보면 답을 찾을 수 있었다.

```swift
tableView.delegate = self
```

delegate는 클래스안에 생성해서 사용하는 게 아닌 다른 객체에게 할당 받아서 사용하는 방식이다. 
weak var로 클래스 내부에서 생성하면, 레퍼런스가 생성되는 동시에 할당하는 기이한 현상이 발생한다. 

<img src="/Users/yun/Library/Application Support/typora-user-images/image-20200628142422389.png" alt="image-20200628142422389" style="zoom:50%;" />

그렇기 때문에 코드로 view를 생성할 때 외부에서 주입하는 형식이 아니면 weak var를 사용할 수 없다. 

