### Singly LinkedList
In case of linkedlist, we basically create a Node which holds data and another node inside it which is named as next. Though, internally since java is passed by reference hence we say that next is actually the pointer point to next node. 
Now, as we have node in place, hence in order to create singly linkedlist we can simply define a node instance and can name it as head. 
 
### Insertion into singly linked list
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
In order to print, while the head node is null. We will keep on iterating it by assigning the current node next value into it. Untill, it is null we will keep on printing it. 
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

```

```
