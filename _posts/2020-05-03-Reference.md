---
layout: post
title:  "Reference"
date:   2020-05-03 23:12:00 
categories: iOS

---

문득 stroyboard에 객체를 IBOutlet으로 연결하면 기본적으로 weak로 선언되었고, weak를 지우고 strong으로 선언해도 차이가 보이지 않았다. class를 사용을 지양하라는 말만 읽었었고, reference count를 0으로 만들지않으면 memory lick이 발생한다고 읽었었다. 그래서 코드로 view객체를 생성할때 기본적으로 strong이 아닌 weak로 변경해야 겠다는 생가이 들어서 weak로 변경했다.

``` swift
    private weak var label: UILabel! = {
        let label = UILabel()
        label.textAlignment = .center
        label.font = UIFont.boldSystemFont(ofSize: UIFont.boldTitleSize)
        return label
    }()

```

프로젝트를 런했을때 오류가 발생했었고 그 이유는 label이 해제(nil) 되었다. 스토리 보드에서 IBOutlet으로 연결 했을때는 weak와 strong 둘다 사용 가능했지만, 코드로 생성했을 때는 weak로 선언하면 에러가 발생하는 이유가 궁금했다.

그 이유는 생각보다 간단했다. 기본적으로 delegate pattern을 적용할 때  아래와 같이 weak와 optional을 붙인다. 다른 객체로 부터 reference가 발생하고 retain cycle을 피하기 위해서 weak, optionalDㄴㅋ2ㅇ34567ㅡ,[}|[];

\ㅔㅣ}{?j.흐 ㅜ75ㄴㅍㅊ4ㅌ3ㄴ2ㅋㅁㄴ3}]

```swift
weak var delegate: SomeDelegate?
```



흔히 우리가 아는 stroyboard는 XML파일이며 

<!--more-->

