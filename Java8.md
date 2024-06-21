### Find the frequency of characters from the list of string 
It is easy to find the frequency of string but as we have to been asked to find the frequency of character Hence, we will have to first convert the list of string into the 
list of characters and in order to do so, we will be using flatmap() and inside it we will first convert the string into the stream of characters and then we will it to object wherein
internally we will casting it char. 
```
 List<String> stationeryList = Arrays.asList("Pen", "Eraser", "Note Book", "Pen", "Pencil", "Stapler", "Note Book", "Pencil");
 stationeryList.stream().flatMap(x->x.chars().mapToObj(y->(char)y)).collect(Collectors.groupingBy(Function.identity(),Collectors.counting()));
Output: { =2, a=2, B=2, c=2, E=1, e=8, i=2, k=2, l=3, N=2, n=4, o=6, p=1, P=4, r=3, S=1, s=1, t=3} 
```
### Find the list of numbers which starts from 1.
Herein, we will be converting the integers to String and then we will have access of all the methods which are present in the String class.
```
List<Integer> list1 = Arrays.asList(11,12,34);
list1.stream().map(x->x+"").filter(x->x.startsWith("1")).collect(Collectors.toList())
```
### Find the sum of int list 
Sum() method is not there in the stream class, Hence first map it to Integer then we can invoke sum method.
```
List<Integer> list1 = Arrays.asList(11,12,34);
list1.stream().mapToInt(x->x).sum()
```
### Find the sum of int list without using sum method
We can not use normal wrappers like Integer because while processing in stream to avoid any modification we are forced to use final variable or atomic variables.  
The primary use of AtomicInteger is when you are in a multithreaded context and you need to perform thread safe operations on an integer without using synchronized. 
```
 AtomicInteger sum = new AtomicInteger();
List<Integer> list1 = Arrays.asList(2,3,4);
list1.stream().forEach(x->{
            sum.addAndGet(x);
        });
System.out.println(sum);
```
### Find kth max and kth min
```
//Minimum
List<Integer> list1 = Arrays.asList(2,3,4,5,6,7);
list1.stream().sorted().skip(k-1).findFirst().get();
Output: 3
```
```
//Maximum
 List<Integer> list1 = Arrays.asList(2,3,4,5,6,7);
list1.stream().sorted(Comparator.reverseOrder()).skip(k-1).findFirst().get();
Output: 6
```
### There is a list employee wherein there is a instance as address (has city and pincode), you have to group them on the basis on pincode
```
List<Employee> list = new ArrayList<>();
list.add(new Employee("A", new Address("City1", 452)));
list.stream().collect(Collectors.groupingBy(x->x.getAddress().getPincode()));
```

### Find the most frequent element in the list
Herein, we will first find the frequency of each digit and then we will again stream() the resultant map and will invoke max() which takes comparator as the input param. In order to pass comparator in the max funxtion then we can also pass two variable which would be basically 
representing two different map and then using compareTo method we will be making comparison.
```
 List<Integer> list1 = Arrays.asList(2,3,4,5,6,7,7);
list1.stream().collect(Collectors.groupingBy(x->x,Collectors.counting())).entrySet().stream().max(Map.Entry.comparingByValue()).get().getKey();
//OR
list1.stream().collect(Collectors.groupingBy(x->x,Collectors.counting())).entrySet().stream().max((x,y)-> y.getValue().compareTo(y.getValue()).get().getKey();
```
### Partition negative and positive numbers  
```
Map<Boolean, List<Integer>> collect = list1.stream().collect(Collectors.partitioningBy(x->x>0));
Output: {false=[-7, -1], true=[2, 3, 4, 5, 6, 7, 7]}
```
### Remove special character from string
```
str.chars().mapToObj(x->(char)x).filter(x->x>=65 && x<=122 || x==32).forEach(System.out::print);
```

### Shift zero rightward
Here significant thing is boxed() which is used to convert a stream of primitive values (such as int, long, or double) into a stream of their corresponding wrapper class objects (Integer, Long, or Double).
```
int[] arr={3,2,4,5,7,0,0,1,2};
List<Integer> collect = Arrays.stream(arr).filter(x -> x >=0).boxed().sorted(Comparator.reverseOrder()).collect(Collectors.toList());
```
















