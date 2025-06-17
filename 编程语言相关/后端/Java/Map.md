## computeIfAbsent()

### 作用

判断一个map中是否存在这个key，
如果存在则处理value的数据，
如果不存在，则创建一个满足value要求的数据结构放到value中。

### 示例

不使用`computeIfAbsent()`
```java

public class TestComputeIfAbsent {
  static HashMap<String, Set<String>> hashMap = new HashMap<>();
  public static void main(String[] args) {
    Set<String> set = new HashSet<>();
    set.add("zhangSan");
    hashMap.put("china", set);
    // 判断map中是否存在，如果存在则添加元素到set中，如果不存在则新建set添加到hashMap中
    if(hashMap.containsKey("china")) {
      hashMap.get("china").add("liSi");
    } else {
      Set<String> setTmp = new HashSet<>();
      setTmp.add("liSi");
      hashMap.put("china", setTmp);
    }
    System.out.println(hashMap.toString());
  }

```

使用`computeIfAbsent()`
```Java
public class TestComputeIfAbsent {
  static HashMap<String, Set<String>> hashMap = new HashMap<>();
  public static void main(String[] args) {
    Set<String> set = new HashSet<>();
    set.add("zhangSan");
    hashMap.put("china", set);
    // after JDK1.8
    hashMap.computeIfAbsent("china", key -> getValues(key)).add("liSi");
    System.out.println(hashMap.toString());
  }
 
  public static HashSet getValues(String key) {
    return new HashSet();
  }
}

```
