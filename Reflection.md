###
```
package Reflection;

import java.lang.reflect.Field;
import java.util.*;
import java.util.stream.Collectors;

public class CheckException <T>{

    public HashMap<String, Object> check(T wrapper) throws IllegalAccessException {
    Field[] fields= wrapper.getClass().getDeclaredFields();
          Field field = Arrays.stream(fields).filter(x -> x.getName().equals("additionalProperties")).findFirst().orElseThrow();
        return (HashMap<String, Object>) field.get(wrapper);
    }

    public List<String> checkNullValues() throws IllegalAccessException {
        CheckException<Wrapper> obj=new CheckException<>();
        Wrapper wrapper=new Wrapper(new HashMap<>());
        HashMap<String, Object> testMap = obj.check(wrapper);
        return testMap.entrySet().stream().filter(x -> x.getValue() == null).map(x -> x.getKey()).collect(Collectors.toList());
    }



    public static void main(String[] args) throws IllegalAccessException {
        CheckException<Wrapper> obj=new CheckException<>();
        Wrapper wrapper=new Wrapper(new HashMap<>());
        System.out.println(wrapper);
//      //  Set<String> values = obj.check(wrapper).keySet();
         HashMap<String, Object> testMap = obj.check(wrapper);
        System.out.println(obj.checkNullValues());
        List<String> list=obj.checkNullValues();

   // List<Integer> liist=Arrays.asList(2,3,2,1,2);
        List<List<String>> parent = new ArrayList<>();

// Initialize child array
        List<String> child = new ArrayList<>();
        child.add("one");
        child.add("two");
        List<String> child1 = new ArrayList<>();
        child1.add("three");
        child1.add("four");
        parent.add(child1);
        parent.add(child);

     //   System.out.println( parent.stream().flatMap(x->x.stream()).collect(Collectors.toList()));
        System.out.println( parent.stream().flatMap(Collection::stream).collect(Collectors.toList()));

     //   System.out.println(parent);



       // Set<Map.Entry<String, Object>> collect = testMap.entrySet().stream().filter(x ->x.getValue().toString()!=null).collect(Collectors.toSet());
       // System.out.println(collect.stream().filter(x->StringUtils.isNotEmpty(x.getKey())).collect(Collectors.toList()));

    }

}

```

```
package Reflection;

import lombok.Data;
import lombok.ToString;

import java.util.ArrayList;
import java.util.HashMap;

@Data
@ToString
public class Wrapper {
 // Some instance varianle 

    HashMap<String,Object> additionalProperties;

    public Wrapper(HashMap<String, Object> additionalProperties) {
        additionalProperties.put("check", "baba");
        additionalProperties.put("wake", "baba");
        additionalProperties.put("fake", "baba");
        additionalProperties.put("lake", null);
        additionalProperties.put("bake", null);
        this.enbid=1;
        this.additionalProperties = additionalProperties;
    }

    public Wrapper(){}

}

```
