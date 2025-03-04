## Two pointer with comparison {Two Sum}
Create two pointer which is left and right. 
Sort the array.
Initialize a loop as long as left is less that right. 
If the condition on both pointer exceeds the target then decrease the right pointer.
If the condition on both pointer subceed the target then increase the left pointer. 
If matches then return it. 
```
 public static int[] check(int[] arr, int target){
 int left =0;
    int right = arr.length-1;
    int[] array= new int[2];
    int counter=0;
    Arrays.sort(arr);
 while (left < right){
        if(arr[left]+arr[right]>target){
            right--;
        } else if (arr[left]+arr[right]<target) {
            left++;
        } else if (arr[left]+arr[right]==target) {
            array[counter] = arr[left];
            counter++;
            array[counter] = arr[right];
            return array;
        }else {
            throw new RuntimeException("Cannt found");
           }
    }
return array;
    }
```
```
    public boolean check(int[] arr, int k){
        HashMap<Integer, Integer> hm = new HashMap<>();
        boolean flag=false;
        for(int i=0;i<arr.length;i++){
            int comp=k-arr[i];

            if(hm.containsKey(arr[i])){
                flag= true;
                break;
            }
            hm.put(comp,i);
        }
        return flag;

    }
```
## RemoveDuplicateFromSortedArray {Move Unique Element to Front}
Sort the Array. 
Start traversing from first index and check whether present one is different than the current one and 
if true then move it to the front place.
```
public void check(int[] arr, int k){
        Arrays.sort(arr);
        int j=0;
        for(int i=1;i< arr.length;i++){
            if(arr[i]!=arr[j]){
                arr[j]=arr[i];
                j++;
            }
        }
    }

```
## Check if sorted or not
start traversing from first index and check if the 
element at zero index is greater than one at first index
If true then turn the flag of asc to false
check same for desc. Herein we are checking if it is not ascending then it is descending. 
```
public boolean check(int[] arr){
        boolean asc=true;
        boolean desc=true;
        for(int i=1;i< arr.length;i++){
            if(arr[i]>arr[i-1]){
                desc= false;
            }
            if(arr[i]<arr[i-1]){
                asc=false;
            }
        }
        return asc || desc;
    }

```
## Shift zeroes  
One pointer is being used here with the swap function. 
Traverse and keep the condition that the current pointer should not go beyond the another pointer.
If current one is equal to zero then swap. 
For leftward, just start the pointer from zero and no need to put any extra condition. 
```
// For rightward
public int[] check(int[] arr, int k){
        int j=arr.length-1;
      for(int i=0;i<arr.length & i< j;i++){
          if(arr[i]==0){
              swap(arr,i,j);
              j--;
          }
      }
      return arr;
        }
// For leftward
public int[] check(int[] arr, int k){
        int j=0;
      for(int i=0;i<arr.length;i++){
          if(arr[i]==0){
              swap(arr,i,j);
              j++;
          }
      }
      return arr;
        }
```
## Union of Array {Using HashMap}
Herein, create a hashmap and get all the elements of Array stored there in hashmap while storing make sure to increase the frequency of value. 
```
static ArrayList<Integer> check(int[] arr, int[] arr1){
        HashMap<Integer, Integer> hs = new HashMap<>();
        for(int i: arr){
            if(hs.containsKey(i)){
                hs.put(i,hs.get(i)+1);
            }else {
                hs.put(i,1);
            }
        }
        for(int i: arr1) {
            if (hs.containsKey(i)) {
                hs.put(i, hs.get(i) + 1);
            } else {
                hs.put(i, 1);
            }
        }
        ArrayList<Integer> AL=new ArrayList<>();
        for(var j : hs.keySet()){
            AL.add(j);
        }
        return AL;
    }
```
## Boyer-Moore Majority Voting Algorithm {Find Majority Element}
 This algo works in two steps, in first step we check for the possible candidate
  and in second step we verify whether the given candidate appears more than the given time
 
  In first step, we first checks whether the first element is equal to the traversing element as long as
  the current pointer matches, we increase the counter and if it does not match then we decrease the counter
 In the situation wherein this counter gets zero then we instantly increase the majority element
 and same thing goes on....
 Point to be noted is, we are discarding the subarray wherein the majority of element is not present and moving to new sub-array
```
public class MooresVotingAlgo {

public int findCandidate(int[] arr){
        int maj=0;
        int count=1;
        for(int i=0; i<arr.length;i++){
            if(arr[i]==arr[maj]){
                count++;
            }else{
                count--;

            }
            if(count==0){
                maj=i;
                count=1;
            }
        }
        return arr[maj];
    }

    public int isMajority(int[] arr, int maj){
        int n=arr.length/2;
        int count=0;
        for(int i=0; i< arr.length;i++){
            if(arr[i]==maj){
                count++;
            }
            if(count >n){
                return maj;
            }
        }
        return -1;
    }


    public static void main(String[] args) {
        int[] arr= {2,4,2,3,2,2,1};
        System.out.println(new MooresVotingAlgo().isMajority(arr,new MooresVotingAlgo().findCandidate(arr)));

    }
}

```
## Check whether the sum of subarray is zero or not
To check the sum of subarray, we can create a variable named as sum and will continiously adding each value into it and at the same time, we will be adding it into the set. Finally, we will check If the the current sum is already there in the hashset then we can return true right away. Point to be noted, if the current sum is already there in the set then it means that the present value would have reduced it to the previous sum, hence it means that if it would have summed up then  the resulatant would have been zero.  
```
   public boolean check(int[] arr) {
        Set<Integer> hs = new HashSet<>();
        int sum = 0;
        for (int j = 0; j < arr.length; j++) {
            sum = sum + arr[j];
            hs.add(sum);
            if (sum == 0 || hs.contains(sum)) {
                return true;
            }
        }
        return false;
    }

int[] yash={1,2,3,-3,1,-2};

```
## Kadane's Algorithm (Maximum sum of contagious subarray)
Here, we will iterate the given array with a single loop and while iterating we will add the elements in a sum variable. Now, if at any point the sum becomes less than 0, we will set the sum as 0 as we are not going to consider any subarray with a negative sum. Among all the sums calculated, we will consider the maximum one. Herein, we are basically discarding the array which is moving towards zero or negative value. 
```
public int check(int arr[]){
    int max=0;
    int sum=0;
    for(int i=0; i< arr.length;i++){
        if(arr[i]!=0) {
            sum = sum + arr[i];
            if (sum > max) {
                max = sum;
            }
        }
       if(sum<0){
           sum=0;
       }

    }
    return max;
}

```


## Find K largest element (Using Min-heap) (By Default PQ uses min-heap)
It can be easily solved using minheap or priority queue, we will just have to add all the elements in priority queue and will have to check If the size of the priority queue exceeds the k then poll the elements or remove the elements. 
```
public void find(int[] arr, int k){
        PriorityQueue<Integer> pq= new PriorityQueue<>();
        for(int a:arr){
            pq.add(a);

            if(pq.size()>k){
                pq.poll();
            }

        }
        System.out.println(pq);
    }
  int[] arr={4,5,8,99,100,6,7};
  Output: [99, 100];
```
## Find K smallest element (Using max-heap)  
It can also be done as presviously, just we will have to pass the comparator to PQ in order to convert it into Max-Heap;
```
public void find(int[] arr, int k){
        PriorityQueue<Integer> pq= new PriorityQueue<>(Comparator.reverseOrder());
        for(int a:arr){
            pq.add(a);

            if(pq.size()>k){
                pq.poll();
            }

        }
        System.out.println(pq);
    }

   int[] arr={4,5,8,99,100,6,7};
   Output: [5, 4]
```
## Find K largest element from sorted array (Using binary search) 
Here, we will be directly dealing with the elements intead of their indices. First, we will assign the lowest and highest value to low and and high pointer, we will achieve by traversing and comparing the whole array. Now, we will run a loop and will check; how many elements do we have which is higher than the middle element and whether the count of this elements is higher  or lower than the k or not. If It is higher than k then we will make the low as pointer as mid+1 or If it is not true then we will make the high pointer mid-1;
```
    public static int findKthLargest(int[] arr, int n,
                                     int k) {

        int low = Integer.MAX_VALUE;
        int high = Integer.MIN_VALUE;
        for (int a : arr) {
            low = Math.min(a, low);
            high = Math.max(a, high);
        }

        while(low<=high){
        int count = 0;
        int mid = low + (high - low) / 2;
        for (int a : arr) {
            if (a > mid) {
                count++;
            }
        }


        if (count >= k) {
            low = mid + 1;
        }
     else {
            high = mid - 1;
        }
    }

        // Return the Kth largest element
        return high;
    }
```
## Find the length of longest consecutive sequence
[Brute force approach]: Herein we can iterate a loop wherein we will first choose the first element and then we will be checking the exact next element(x+1) in the given array and if we find it then we will increase the counter and the chosen element by 1. We will also
maintain a seperate counter which would be updated by comparing the maximum value with the count variable.
```
   public boolean find(int[] a, int k){
        for(int i=0; i<a.length;i++){
            if(a[i]==k){
                return true;
            }
        }
        return false;
    }
  public int longestSubSeq(int[] arr){
        int n = arr.length;
        int longest=1;
        for(int i=0; i<n;i++){
            int x=arr[i];
            int count=1;
            while(find(arr,x+1)==true){
                count++;
                x=x+1;
            }
            longest = Math.max(longest, count);
        }
        return longest;
    }
```
[Optimal Approach]: We can get all the elements stored in the hashmap or hashset and then we can check for the next element in comparison
to the choosen element in the hashmap and if It is found then we can increase the counter (Remember to keep your counter outside the loop as it will get updated with assigned value after each iteration). This checking would be done inside the for loop
and we will be keep on checking the consecutive element. 
```
public int longestSubSeq(int[] arr){
        int n = arr.length;
        int longest=1;
        HashMap<Integer, Integer> hm = new HashMap<>();
        for(int i=0; i<n;i++){
            if(hm.containsKey(arr[i])){
                hm.put(arr[i],hm.get(arr[i]+1));
            }else {
                hm.put(arr[i],1);
            }
        }
        int count=1;
        for(int i=0; i<n;i++){
            int x=arr[i];
            if(hm.containsKey(x+1)){
                count++;
            }
            longest = Math.max(count, longest);
        }

        return longest;
    }
```
## Remove odd numbers from arraylist
It is a  tricky question with the simple logic. If you will run a loop to filter out the even number from 0 to n then whenever you remove any element the indices are shifted which sometimes skips the elements and causes problem. Hence, the simple solution is to run the loop in the reverse order from n to 0, It would change the indices in the backward direction hence would not affect elements. 
## Find first and last index of an element in the array (O(n))
Create two variables first and last and assign -1 value to it. Now iterate the array and check if the current element is not equal to target then continue the iteration and if the condition gets false then check if the first variable is equal to -1 and if true then assign the value else assign the current index value to last.
```
 public void check(int[] arr, int  k){
        int first =-1;
        int last =-1;
        for(int i=0; i< arr.length;i++){
            if(arr[i]!=k){
                continue;
            }
            if(first==-1){
                first=i;
            }else{
                last=i;
            }

        }
        System.out.println(first +"  "+last);
    }
```
## Find first and last index of an element in the array (O(log(n)))

```
```
## Find the sum of k largest element (O(n^2))
```
 public int find(int[] arr, int k){
        ArrayList<Integer> al = new ArrayList<>();
        int max=0;
        for(int i=0; i< arr.length-k+1;i++){
            int sum=0;
            for(int j=i; j< i+k;j++){
                sum=sum+arr[j];
            }
            if(sum>max){
                al.add(sum);
                max=sum;
            }

        }
        return al.stream().max(Integer::compare).get();
    }
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```

## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```
## 
```
```






















## Time Complexity

O(1) no matter how many items you have to sort, it'll take the same amount of time
O(logn)  doesn't grow very quickly with input size. It's like having a phonebook and being able to find a name quickly by splitting it in half repeatedly.
O(n) If you double the input size, it will take roughly twice as long to run. It's like checking each item in a list one by one.
O(n^2)   If you double the input size, it will take about four times as long to run.

## Recursion
Recursion is useful in solving problems which can be broken down into smaller problems of the same kind. Recursion uses more memory, because the recursive function adds to the stack with each recursive call, and keeps the values there until the call is finished. The recursive function uses LIFO (LAST IN FIRST OUT) Structure just like the stack data structure.

## Arrays:

Use arrays when you need constant-time access to elements using an index.
Use arrays when the size of the data is fixed, and you don't need to insert or delete elements frequently.

## Linked Lists:

Use linked lists when you need frequent insertions or deletions from the middle of the list.
Use linked lists when you have an unknown or frequently changing size of data.

## Stacks:

Use stacks when you need last-in, first-out (LIFO) behavior.
Use stacks for function calls, parsing expressions, or managing undo functionality.

## Queues:

Use queues when you need first-in, first-out (FIFO) behavior.
Use queues for tasks like managing requests, breadth-first search, or implementing a print spooler.

## Hash Tables:

Use hash tables for constant-time average-case lookup, insert, and delete operations.
Use hash tables when you need a collection of key-value pairs and the keys are unique.

## Trees (Binary Trees, Binary Search Trees, AVL Trees, etc.):

Use binary trees for fast search, insert, and delete operations in a sorted collection of elements.
Use different types of trees based on specific requirements, such as balanced trees for maintaining balance in height.

## Heaps (Binary Heaps, Fibonacci Heaps, etc.):

Use heaps for optimizing operations like finding the minimum or maximum element efficiently.
Use heaps in priority queues or scheduling algorithms.

## Graphs (Adjacency Matrix, Adjacency List, etc.):

Use graphs when you need to represent relationships between entities.
Use adjacency lists for sparse graphs, and adjacency matrices for dense graphs.

## Tries:

Use tries when dealing with problems involving strings or a set of words.
Tries are particularly useful for implementing dictionaries or spell-checking systems.

## Sets and Maps:

Use sets and maps when you need to store unique elements and associate values with keys, respectively.
Use sets for checking membership, and maps for key-value associations.
