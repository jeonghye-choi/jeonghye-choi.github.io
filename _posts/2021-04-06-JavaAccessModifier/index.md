---
title: Java, Access Modifier(접근제어자)
date: 2021-04-06
tags:
  - Java
keywords:
  - Java
  - 접근제어자
---

## 접근제어자

1. private

2. default

3. protexted

4. public

### private

private가 붙은 변수, 메소드는 해당 클래스에서만 접근 가능.

```java
public class AccessModifier {
    private String secret;
    private String getSecret(){
        return this.secret;
    }
}
// secret변수, getSecret매소드는 오직 AccessModifier 클래스에서만 접근 가능
```

### default

접근제어자를 별도로 설정하지 않는다면, default 접근제어자로 됨.

이는 해당 패키지 내에서만 접근이 가능.

```java
// AstreetHouse.java
package jeonghye.hometown;

public class AstreetHouse {
    String ownerName = "Kim";
}
```

```java
// BstreetHouse.java
package jeonghye.hometown;

public class BstreetHouse {
    String ownerName = "Park";

    public static void main(String[] args){
        AstreetHouse aHouse = new AstreetHouse();
        System.out.pringln(aHouse.ownerName);
    }
}

```

### protected

동일 패키지내의 클래스 뿐만아니라 해당 클래스를 상속받은 외부 패키지의 클래스에서 접근 가능

```java
// AstreetHouse.java
package jeonghye.hometown;

public class AstreetHouse {
    protected String ownerName = "park";
}
```

```java
// JinaPark.java
package jeonghye.hometown.person;

import hometown.AstreetHouse;

public class JinaPark extends AstreetHouse {
    public static void main(String[] args){
        JinaPark jnp = new JinaPark();
        System.out.println(jnp.ownerName);
    }
}

```

### public

어떤 클래스에서라도 접근 가능

```java
package jeonghye.house;

public class AstreetHouse {
    protected String owner = "park";
    public String info = "this is public message.";
}
```
