# 資料流替代方案

[RxJava](RxJava) 已經介紹了資料流的概念。如果你不需要 RxJava  提供的執行緒管理、錯誤處理等又覺得 RxJava 不夠輕量。或許你可以採用輕量，只針對資料流的函式庫。

## StreamSupport

After:

```java
RefStreams.of("one", "two", "three", "four")
    .filter(e -> e.length() > 3)
    .peek(e -> System.out.println("Filtered value: " + e))
    .map(String::toUpperCase)
    .peek(e -> System.out.println("Mapped value: " + e))
    .collect(Collectors.toList());
```

After:

```java
public static List<String> getNames(List<User> users) {
    return StreamSupport.stream(users).map(user -> user.name()).collect(Collectors.toList());
}
```

After:

```java
public static String[] getNames(User[] users) {
    return J8Arrays.stream(users).map(user -> user.name()).toArray(length -> new String[length]);
}
```

## 其他方案

* https://github.com/kgmyshin/Marray
* https://github.com/konmik/solid
* https://github.com/goldmansachs/gs-collections

特點：

* Marray 可修改
* SolidList 主要以 ImmutableList 出發，所以沒實現修改能力
* SolidList 支援 Parcelable 傳遞
* 知名 gs-collections 不過似乎不夠輕

另外還有其他 Promise 選用:

* [Bolt-Android](bolts-android.md)

## See Also

* https://sourceforge.net/projects/streamsupport/
* https://github.com/yongjhih/streamsupport
* http://verhoevenv.github.io/2015/08/18/fluentiterable-streamsupport-java8.html
* https://github.com/goldmansachs/gs-collections
* http://www.goldmansachs.com/gs-collections/documents/GS%20Collections%20Training%20Session%20and%20Kata%205.0.0.pdf
