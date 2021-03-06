---
layout: post
title: Java | Immutable & Mutable
author: yoon1fe
color: tomato
tags: [Java]
#feature-img: "assets/img/feature-img/playmuseum.jpg"
#thumbnail: "assets/img/thumbnails/feature-img/playmuseum.jpg"

excerpt_separator: <!--more-->
---

<!--more-->


## [불변 객체 (Immutable)]

불변 객체란 **한 번 객체가 생성되면 변하지 않는 객체**를 의미합니다. Java의 대표적인 불변 객체는 **String** 클래스, **Integer, Long**과 같은 Wrapper Class (Boxed primitive object) 들이 있습니다.


<br>
### String 클래스

String 클래스를 한 번 봅시다.

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
    
	/* ... */
    
    public String() {
        this.value = "".value;
    }
}
```
<br>
필드의 접근 제한자는 private이며, **final** 키워드를 통해 변수를 변경할 수 없도록 제한되어 있습니다. 이처럼 String 클래스는 Immutable하기 때문에 새로 수정할 때마다 기존 메모리를 버리고 새로운 메모리에 값을 넣어서 연결합니다. 따라서 **메모리 누수가 발생할 수 있고, 새로운 객체를 계속 생성해야 하기 때문에 성능 저하가 발생**할 수 있습니다.<br><br>

#### 그럼, **String 클래스는 왜 Immutable 할까요 ?**


String 변수의 reference를 여러 곳에서 갖고 있을 때, String이 mutable하다면 String 값 변경 시 이를 참조하는 모든 곳에서 변경된 object를 공유하게 됩니다. 이는 예상치 못한 문제를 만들어 낼 수 있으므로 Java의 String 클래스는 Immutable한 것입니다.


<br>

#### Immutable한 객체를 사용함으로써 얻을 수 있는 이점

Java에서는 cloneable 인터페이스를 구현함으로써 deep copy를 하지 않는 이상 모든 값이 reference로 전달되므로 같은 객체를 가리키게 됩니다.<br>
가리키는 대상이 mutable하다면 필드를 변경하는 메소드를 호출했을 때 reference를 가지고 있는 모든 곳에서 내가 원하는 상태임을 보장할 수 없습니다. immutable한 객체를 사용하면 reference로 인한 다양한 side-effect를 미리 방지할 수 있습니다. 또한, 멀티 쓰레드 환경에서도 따로 동기화 처리할 필요없이 객체를 공유해도 되겠죠.

> 방어적 복사본을 만들 수고를 덜어주고, 다중 쓰레드 환경에서도 안전합니다.

- JDK 1.5 버전부터는 String + String 연산이 새로운 메모리에 저장되는 성능 이슈를 개선하기 위해 컴파일 단계에서 StringBuilder로 컴파일된다고 합니다.!


<br>
## [가변 객체 (Mutable)]

가변객체는 **객체가 생성된 후에도 필드 값이 변경될 수 있는 객체**입니다. 필드 값을 바꿀 수 있는 메소드를 제공합니다. 가변 객체의 예로는 String 클래스와 반대로 **StringBuilder** 클래스가 있습니다.


**AbstractStringBuilder 클래스 (StringBuilder 클래스가 상속하는 추상 클래스)**

```java
abstract class AbstractStringBuilder implements Appendable, CharSequence {
    /**
     * The value is used for character storage.
     */
    char[] value;
}
```

StrinBuilder 클래스에서 문자열을 저장하는 변수 value는 mutable하기 때문에 String 클래스와 달리 final 키워드가 없답니다 !



<br>
<br>
<br>

##### Reference
##### [[Java] Immutable Class (불변 클래스)](https://limkydev.tistory.com/68){:target="_blank"}
##### [mutable 과 immutable](https://hun-developer.tistory.com/2?category=772082){:target="_blank"}