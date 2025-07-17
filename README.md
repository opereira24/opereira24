# My Java Doc

## Index
- [Arrays](#arrays)
- [List](#list)
- [Set](#set)
- [Map](#map)
- [Non-Primitive Types and Common Methods](#non-primitive-types-and-common-methods)
- [Streams](#streams)
- [Switch Expression](#switch-expression)

---

# Arrays
[☝️](#index)

## Common utility methods
```java
int[] a = {3, 1, 2};
Arrays.sort(a);                      // a = [1, 2, 3]

int[] x = {1, 2, 3};
int[] y = {1, 2, 3};
boolean eq = Arrays.equals(x, y);    // true

int[] original = {5, 6};
int[] copy = Arrays.copyOf(original, 4);  // [5, 6, 0, 0]
```

## Conversion between Array and List
```java
// Array to List (fixed-size)
List<String> list = Arrays.asList(array);

// List to Array
String[] array = list.toArray(new String[0]);
```  

## Static Initialization
```java
int[] a = {1, 2, 3};
String[] names = {"Ines", "Goncalo", "Leonor"};
```

## Initialization with new + values
```java
int[] a = new int[]{1, 2, 3};
```

## Initialization with new + size
```java
int[] a = new int[3];       // [0, 0, 0]
String[] names = new String[2];  // [null, null]
```

## Multidimensional initialization
```java
int[][] matrix = new int[2][3];
int[][] matrix2 = {{1, 2}, {3, 4}};
```

---

# List
[☝️](#index)

## Common utility methods
```java
List<String> list = new ArrayList<>(List.of("b", "a", "c"));
Collections.sort(list);                   // list = [a, b, c]
Collections.reverse(list);                // list = [c, b, a]
Collections.shuffle(list);                // random order
boolean has = Collections.disjoint(list, List.of("x"));  // true if no common elements
```

## Main List Types
- `ArrayList`: fast access, slow insert/remove in the middle
- `LinkedList`: good for frequent insert/remove, slow access
- `Stack`: extends `Vector`, LIFO behavior (push/pop)

## Conversion between List and Array
```java
// List to Array
String[] array = list.toArray(new String[0]);

// Array to List (immutable or fixed-size)
List<String> list = List.of(array);
List<String> list2 = Arrays.asList(array);
```

## Initialization with values
```java
List<String> list = List.of("a", "b", "c");  // immutable
List<String> list2 = Arrays.asList("a", "b", "c");  // fixed-size
```

## Empty initialization
```java
List<String> list = new ArrayList<>();
List<Integer> numbers = new LinkedList<>();
Collections.emptyList();    // immutable list
```

## Add elements
```java
list.add("value");
```

## Iterate
```java
for (String s : list) {
    System.out.println(s);
}

list.forEach(System.out::println);
```

## Modify
```java
list.set(0, "new value");
list.remove("a");
```

## Sort
```java
Collections.sort(list);  // natural order
list.sort(Comparator.reverseOrder());
```

## Check existence
```java
list.contains("value");
```

---

# Set
[☝️](#index)

## Common utility methods
```java
Set<String> set = new HashSet<>(Set.of("a", "b"));
boolean disjoint = Collections.disjoint(set, Set.of("x"));  // true
Set<String> s1 = new HashSet<>(Set.of("a", "b", "c"));
Set<String> s2 = Set.of("b", "c", "d");
s1.retainAll(s2);   // s1 = [b, c]
s1.removeAll(s2);   // removes common elements
s1.addAll(s2);      // adds elements from s2
```

## Main Set Types
- `HashSet`: no duplicates, no order guarantee
- `LinkedHashSet`: maintains insertion order
- `TreeSet`: sorted, no duplicates

## Initialization
```java
Collections.emptySet();          // immutable set
Set<String> set = new HashSet<>();
Set<String> set2 = new TreeSet<>();
```

## Add and remove
```java
set.add("value");
set.remove("value");
```

## Check existence
```java
set.contains("value");
```

## Iterate
```java
for (String s : set) {
    System.out.println(s);
}

set.forEach(System.out::println);
```

---

# Map
[☝️](#index)

## Common utility methods
```java
map.putIfAbsent("a", 1);
map.getOrDefault("b", 0);            // returns 0 if key "b" not present
map.replace("a", 2);                 // replaces value for key "a"
map.keySet();
map.values();
map.entrySet();
```

## Main Map Types
- `HashMap`: no order, fast lookup
- `LinkedHashMap`: maintains insertion order
- `TreeMap`: sorted by key

## Initialization
```java
Collections.emptyMap();                  // immutable map
Map<String, Integer> map = new HashMap<>();
Map<String, Integer> map2 = Map.of("a", 1, "b", 2);
```

## Add, update and remove
```java
map.put("key", 123);
map.put("key", 456);  // overwrite
map.remove("key");
```

## Access
```java
int value = map.get("key");
boolean exists = map.containsKey("key");
```

## Iterate
```java
for (String key : map.keySet()) {
    System.out.println(key + ": " + map.get(key));
}

map.forEach((k, v) -> System.out.println(k + ": " + v));
```

---

# Non-Primitive Types and Common Methods
[☝️](#index)

## String
```java
String s = "hello";
s.length();
s.toUpperCase();
s.substring(1);
s.contains("el");
s.replace("l", "x");
s.equals("HELLO");
```

## Integer / Double / Long (Wrapper Classes)
```java
Integer i = Integer.valueOf("5");
i.intValue();
Integer.parseInt("123");
Double.parseDouble("3.14");
```

## Boolean
```java
Boolean b = Boolean.TRUE;
b.booleanValue();
Boolean.parseBoolean("true");
```

## Character
```java
Character c = 'a';
Character.isLetter(c);
Character.toUpperCase(c);
```

---

# Streams
[☝️](#index)

```java
List<String> names = List.of("Goncalo", "Ines", "Leonor");
names.stream()
     .filter(n -> n.startsWith("B"))
     .map(String::toUpperCase)
     .forEach(System.out::println);  // Output: BRUNO
```

## Creating Streams
```java
Stream<String> stream = Stream.of("a", "b", "c");
List<String> list = List.of("a", "b");
Stream<String> s = list.stream();
```

## Intermediate Operations (lazy)
- `filter(Predicate)`: filter elements
```java
stream.filter(s -> s.startsWith("A"));
```
- `map(Function)`: transform elements
```java
stream.map(String::toUpperCase);
```
- `sorted() / sorted(Comparator)`: sort
```java
stream.sorted();
stream.sorted(Comparator.reverseOrder());
```
- `distinct()`: remove duplicates
```java
stream.distinct();
```
- `limit(n)`, `skip(n)`: limit or skip elements
```java
stream.limit(5);
stream.skip(2);
```

## Terminal Operations
- `forEach(Consumer)`: consume elements
```java
stream.forEach(System.out::println);
```
- `collect(Collectors.toList())`: collect into list
```java
List<String> result = stream.collect(Collectors.toList());
```
- `count()`: count elements
```java
long count = stream.count();
```
- `reduce(...)`: reduce to one result
```java
int sum = stream.reduce(0, Integer::sum);
```
- `anyMatch`, `allMatch`, `noneMatch`: boolean matching
```java
boolean any = stream.anyMatch(s -> s.length() > 3);
boolean all = stream.allMatch(s -> s.startsWith("A"));
boolean none = stream.noneMatch(String::isEmpty);
```

## Examples
### Filter and map
```java
List<String> names = List.of("Goncalo", "Ines", "Leonor");
List<String> result = names.stream()
    .filter(n -> n.length() > 3)
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

### Reduce (sum values)
```java
List<Integer> nums = List.of(1, 2, 3);
int sum = nums.stream().reduce(0, Integer::sum);
```

### Group by
```java
Map<Integer, List<String>> grouped = names.stream()
    .collect(Collectors.groupingBy(String::length));
```

---

# Switch Expression
[☝️](#index)

## Basic switch expression (Java 14+)
```java
String result = switch (day) {
    case MONDAY -> "Start of week";
    case FRIDAY -> "End of week";
    default -> "Midweek";
};
```

## With multiple labels
```java
String type = switch (value) {
    case 1, 2, 3 -> "Low";
    case 4, 5 -> "Medium";
    default -> "High";
};
```
