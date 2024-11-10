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
### LC:2225. Find Players With Zero or One Losses
Herein, we have been given a 2d matrix as input wherein every entry has two value wherein first one tells about won entry and second one about lost entry. We need to find the list of entry which has lost none of the match and which has lost only one match. In  order to solve, first we will maintain the frequency of second element in the hashmap which would be a lostMap with the frequency of number of matches lost, further we can filter the one with desired frequency. Secondly, we will pick the first element and will check whether it is present in lostMap or not and If it is not present then store it as it is the needed answer.

```
public class WinLostMatch {

    public void check(int[][] matches) {
        HashMap<Integer, Integer> lostHm = new HashMap<>();
        for (int[] match : matches) {
            if (lostHm.containsKey(match[1])) {
                lostHm.put(match[1], lostHm.get(match[1]) + 1);
            } else {
                lostHm.put(match[1], 1);
            }
        }
        System.out.println(lostHm);

        List<Integer> lostOnce = new ArrayList<>();
        List<Integer> lostNone = new ArrayList<>();

        for (Map.Entry e : lostHm.entrySet()) {
            if (e.getValue().equals(1)) {
                lostOnce.add((Integer) e.getKey());
            }
        }
        System.out.println(lostOnce);
        for (int[] match : matches) {
            if (!lostHm.containsKey(match[0])) {
                lostNone.add(match[0]);
            }
        }
        System.out.println(lostNone);
    }

    public static void main(String[] args) {
        int[][] matches = {{1, 3}, {2, 3}, {3, 6}, {5, 6}, {5, 7}, {4, 5}, {4, 8}, {4, 9}, {10, 4}, {10, 9}};
        new WinLostMatch().check(matches);
    }
}

output:
 {3=2, 4=1, 5=1, 6=2, 7=1, 8=1, 9=2}
[4, 5, 7, 8]
[1, 2, 10, 10]
```
