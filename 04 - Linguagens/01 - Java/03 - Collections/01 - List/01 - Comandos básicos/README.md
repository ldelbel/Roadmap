# Comandos

## 1. Add 

~~~
public class AddClass { 
    public static void main(String args[]) { 
  
        Collection<String> list = new LinkedList<String>(); 
  
        list.add("A"); 
        list.add("B"); 
        list.add("C"); 
  
        System.out.println("The list is: " + list); 
  
        list.add("Last"); 
        list.add("Elements"); 
  
        System.out.println("The new List is: " + list); 
    } 
} 
~~~

Os termos `Last` e `Elements` são adicionados ao fim da fila. 

## 2. AddAll

~~~ 
import java.util.*; 
  
public class TestClass { 
    public static void main(String[] argv) throws Exception { 

        try { 
            List<String> arrlist = new ArrayList<String>(); 
  
            arrlist.add("A"); 
            arrlist.add("B"); 
            arrlist.add("C"); 
            arrlist.add("Tajmahal"); 
  
            System.out.println("arrlist before operation : " + arrlist); 
  
            boolean b = Collections.addAll(arrlist, "1", "2", "3"); 
  
            System.out.println("result : " + b); 
  
            System.out.println("arrlist after operation : " + arrlist); 
        } 
  
        catch (NullPointerException e) { 
            System.out.println("Exception thrown : " + e); 
        } 
        catch (IllegalArgumentException e) { 
            System.out.println("Exception thrown : " + e); 
        } 
    } 
} 
~~~

Concatenamos com o `addAll` a lista `arrlist` e os termos (em string): `1`, `2`, `3`. 

## 3. Clear

Limpa a lista. 

~~~ 
import java.io.*; 
import java.util.*; 
  
public class TestClass { 
    public static void main(String args[]) { 
  
        Collection<String> list = new LinkedList<String>(); 
  
            list.add("A"); 
            list.add("B"); 
            list.add("C"); 
  
        System.out.println("The list is: " + list); 
  
        list.clear(); 
  
        System.out.println("The new List is: " + list); 
    } 
} 
~~~ 

Output: 
~~~
The list is: [A, B, C]
The new List is: []
~~~ 

## 4. Contains 

Retorna verdadeiro se a lista tiver determinado objeto. 

~~~
import java.io.*; 
import java.util.*; 
  
public class TestClass { 
    public static void main(String args[]) { 
  
        Collection<String> list = new LinkedList<String>(); 
  
        list.add("A"); 
        list.add("B"); 
        list.add("C"); 
  
        System.out.println("The list is: " + list); 
  
        boolean result = list.contains("C"); 
  
        System.out.println("Is 'C' present in the List: " + result); 
    } 
} 
~~~

Output:
~~~ 
The list is: [A, B, C]
Is 'C' present in the List: true
~~~ 

## 5. ContainsAll 

Retorna verdadeiro se a lista tiver todos os elementos presentes em si. 

~~~ 
import java.util.*; 
  
public class ListDemo { 
    public static void main(String args[])  { 

      List<Integer> list = new ArrayList<Integer>(); 
  
        list.add(10); 
        list.add(15); 
        list.add(30); 
        list.add(20); 
        list.add(5); 
  
        System.out.println("List: " + list); 
  
        List<Integer> listTemp = new ArrayList<Integer>(); 
  
        listTemp.add(30); 
        listTemp.add(15); 
        listTemp.add(5); 
  
        System.out.println("Are all the contents equal? " + list.containsAll(listTemp)); 
    } 
} 
~~~ 

Output:
~~~
List: [10, 15, 30, 20, 5]
Are all the contents equal? true
~~~

## 6. Equals

~~~ 
import java.util.Collection;  
import java.util.HashSet;  
public class JavaCollectionEqualsExample2 {  
    public static void main(String[] args) {  
        
        Collection<Integer> collection = new HashSet<>();  
        Collection<Integer> collection1 = new HashSet<>();  
        
        collection.add(5);  
        
        collection1.add(5);  
        collection1.add(8);  
        
        //will return true if both the collections are equal  
       
       boolean val = collection.equals(collection1);  
        System.out.println("Equals methods will return : " + val);  
    }  
}  
~~~ 

Output: 
~~~ 
Equals methods will return : false
~~~ 
A variável `val` retorna falsa porque as listas são diferentes. 

## 7. Hashcode

Dois objetos iguais terão o mesmo hashcode, mas ter o mesmo hashcode não garante que os objetos serão iguais. 

## 8. isEmpty

~~~ 
import java.io.*; 
import java.util.*; 
  
public class TestClass { 
  public static void main(String args[]) { 
  
        Collection<String> list = new LinkedList<String>(); 
  
        list.add("A"); 
        list.add("B"); 
        list.add("C"); 
  
        System.out.println("The list is: " + list); 
  
        System.out.println("Is the LinkedList empty: " + list.isEmpty()); 
  
        list.clear(); 
  
        System.out.println("The new List is: " + list); 
  
        System.out.println("Is the LinkedList empty: " + list.isEmpty()); 
    } 
}
~~~ 

Output:
~~~ 
The list is: [A, B, C]
Is the LinkedList empty: false
The new List is: []
Is the LinkedList empty: true
~~~
