### Singly LinkedList
In case of linkedlist, we basically create a Node which holds data and another node inside it which is named as next. Though, internally since java is passed by reference hence we say that next is actually the pointer point to next node. 
Now, as we have node in place, hence in order to create singly linkedlist we can simply define a node instance and can name it as head. 
 
### Insertion at begining into singly linked list
In order to insert data into linkedlist, we first need to check whether the whole list is empty or not. Hence, we will check the head node and if it empty then assign the new Node with intialized value into it. Else, we will have to iterate the linkedlist wherein we will create a variable which will hold the value of "next" node and we will keep on going deeper till the value of the variable is null. Once, it is null then we can assign our node here. 
```
 public LinkedList insert(LinkedList list, int d){
     Node node = new Node(d);
     if(list.head==null){
         list.head=node;
     }else {
         Node current = list.head;
         while (current.next!=null){
             current=current.next;
         }
         current.next=node;
     }
     return list;
 }
```
### Printing singly linkedlist
In order to print, while the head node is not null. We will keep on iterating it by assigning the current node next value into it. Untill, it is null we will keep on printing it. 
```
public void print(LinkedList list){
     Node current = list.head;
     while (current.next!=null){
         System.out.println(current.data);
         current=current.next;
     }
}
```
### Delete Last Node of Linked List
Herein we just need to check untill the head.next.next==null and once we find it, we can assign the value of head.next to null, in this way the last node will get lost automically.
Two edge cases to consider are:
1. If the input linked list is empty, we return null.
2. If there is only one node in the list, that node itself will be the tail, therefore we return null after deleting that node.
```
    public void deleteTheTail(LinkedList list){
//corner case
     if(list.head==null || list.head.next==null){
         return;
     }
//corner case
     Node current = list.head;
     while (current.next.next!=null){
         current=current.next;
     }
     current.next=null;
    }
```

### Finding element in the linkedList
Just traverse the linkedlist and check for the data and if it is found then return it. 
```
 public boolean find(LinkedList list, int d){
      if(list.head.data.equals(d)){
          return true;
      }else {
          Node current =  list.head;
          while (current!=null){
              if(current.data.equals(d)){
                  return true;
              }
              current=current.next;
          }
      }
      return false;
    }
```
### Size of linkedlist
```
    public int size(LinkedList list){
     Node current = list.head;
     int count =0;
     while(current!=null){
         count++;
         current=current.next;

     }
     return count;
    }
```
## Implement Linked List
```
@Data
@ToString
public class Node {
    int data;
    Node next;
    Node(int d){
        data=d;
        next=null;
    }

}
public class LinkedList {

    Node head ;

    public LinkedList insert(LinkedList list, int d){
        Node node = new  Node(d);
        node.next=null;
        if(list.head==null){
            list.head = node;
        }else{
            Node current= list.head;
            while (current.next!=null){
                current= current.next;
            }
            current.next= node;
        }
        return list;
    }

    public   void show(LinkedList list){
        Node cur= list.head;
        while (cur!=null){
            System.out.println(cur.data);
           cur= cur.next;
        }
    }
}
public class Runner {


    public static void main(String[] args) {
LinkedList list= new LinkedList();
        list.insert(list,1);
        list.insert(list,1);
        list.insert(list,1);
        list.insert(list,1);
        list.insert(list,1);
        list.insert(list,1);

        list.show(list);

    }
}

```
### Find the middle element
In order to find the middle element, first find the size of the linked list and once we have the size then find the middle index and now keep on traversing the linkedlist until the middle element is found. 
```
    public static int size(Node head){
        Node currentNode=head;
        int count=1;
        while (currentNode.next!=null){
            count++;
            currentNode=currentNode.next;
        }
        return count;
    }

    public void findMiddle(Node head){
        int mid = size(head)/2;
        Node currentNode=head;
        while(mid!=0){
            currentNode=currentNode.next;
            mid--;
            if(mid==0){
                System.out.println(currentNode.data);
            }
        }
    }

It can also be resolved using slow and fast poiner technique wherein one pointer would be running twice as faster as slower one. 
```
### Find the middle element using fast and slow pointer or Tortoise-Hare Algorithm
```
    public Node findMiddleUsingFastandSlow(Node head){
        Node fast = head;
        Node slow=head;
        while (fast!=null  ){  //   while (fast != null && fast.next != null && slow != null) {
            slow=slow.next;
            fast=fast.next.next;
        }
     return slow;
    }
```
### Reverse the linkedlist
```
public Node ReverseLinkedList(Node head) {
        Node current = head; // Points to the current node being processed.
        Node prev = null; //  Tracks the previous node in the reversed list. Initially, there is no previous node.
        while(current != null){
            Node front = current.next; // This stores the reference to the next node in the original list, so we don't lose it after reversing the pointer.
            current.next = prev; // This changes the next pointer of the current node to point to the previous node, effectively reversing the link.
            prev = current; // prev moves to the current node to become the new "previous node" for the next iteration.
            current = front; // current moves to the saved next node (front) to continue the traversal.
        }
   return prev; // After the loop, prev points to the new head of the reversed linked list. The function returns prev.
    }
```
```
public LinkedList reverse(LinkedList list){
        Stack<Integer> stack = new Stack<>();
        LinkedList linkedList = new LinkedList();
       Node curr=  list.head;
       while (curr!=null){
           stack.add(curr.data);
           curr=curr.next;
       }
       for(int j=stack.size()-1;j>=0; j--) {
           int i = stack.get(j);
           Node newNode = new Node(i);
           if (linkedList.head == null) {
                linkedList.head=newNode;
           }else {
               Node current= linkedList.head;
               while (current.next!=null){
                   current=current.next;
               }
               current.next=newNode;
           }
       }
       return linkedList;
    }
```
