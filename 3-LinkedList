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
