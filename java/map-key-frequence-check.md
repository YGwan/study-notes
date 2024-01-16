# map

<br>

### key에 해당하는 자료가 몇번 나왔는지 저장하기 위한 Map 사용

``` java
Map<Integer, Integer> map = new HashMap<>();

map.put(a, map.getOrDefault(a, 0) + 1);
map.put(b, map.getOrDefault(b, 0) + 1);
map.put(c, map.getOrDefault(c, 0) + 1);
map.put(d, map.getOrDefault(d, 0) + 1);
```