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
            Node last= list.head;
            while (last.next!=null){
                last= last.next;
            }
            last.next= node;
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
