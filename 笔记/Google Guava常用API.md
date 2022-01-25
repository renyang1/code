# Google Guava常用API

### 1、List相关

#### 分批切割list

**` Lists.partition(List<T> list, int size)`**

**可能的问题**：**`Lists.partition`**返回的切割后的集合其实是使用原集合的引用，最终使用的是List.subList()获取要操作的数据，对切割后的子集合操作会影响原集合，即对切割后的集合进行clear()操作，原集合也会被清空

```java
public static void main(String[] args) {
        List<Integer> integers = Lists.newArrayList(1, 2, 3, 4, 5, 6, 7, 8);
        List<List<Integer>> partition = Lists.partition(integers, 3);
        for (List<Integer> integerList : partition) {
            System.out.println(integerList);
            integerList.clear();
            System.out.println("原集合integers:" + integers);
        }
    }
```

上面的代码会：

Exception in thread "main" java.util.**NoSuchElementException**
	at java.util.AbstractList$Itr.next(AbstractList.java:364)
	at com.ryang.kyapi.guava.ListsTest.main(ListsTest.java:14)

### Map相关





