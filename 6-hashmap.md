### find the number from the list of given number whose frequency is more than twice
```
public class StreamApi {
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(2,3,2,13,2,1);
        long count = list.stream().count();
        Map<Integer, Long> collect = list.stream().collect(Collectors.groupingBy(x -> x, Collectors.counting()));
        System.out.println(collect);
        for(Map.Entry<Integer, Long>  i: collect.entrySet()){
            if(i.getValue()>=2){
                System.out.println(i.getKey());
            }
        }
    }
}
```
### Checking if a Key or Value Exists
```
boolean hasKey = map.containsKey("Apple"); // Returns true
boolean hasValue = map.containsValue(2); // Returns false
```
### Iterating through keys:
```
for (String key : map.keySet()) {
    System.out.println(key);
}
```
### Iterating through values:
```
for (Integer value : map.values()) {
    System.out.println(value);
}
```
### Iterating both at the same time using Entry
```
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```
### 
