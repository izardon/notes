# COMPOSITE

[![hackmd-github-sync-badge](https://hackmd.io/4cnN_jtbTbWJE_3Zo5cZOA/badge)](https://hackmd.io/4cnN_jtbTbWJE_3Zo5cZOA)

###### tags: `Design Pattern`

## Intent:
>*將合成物件結構以樹狀結構表現出它的階層關係，讓 Client 可以用一致的方式看待個體和組成物件。*
>
> - Compose objects into tree structures to represent part-whole hierarchies.
> - Composite lets clients treat individual objects and compositions of objects uniformly.

---
## Motivation

> 通常對合成物件的處理是在合成物件裡直接包含其他原生物件，每個原生物件皆各自獨立，有各自的屬性方法定義。這種情況下合成物件必須針對每個原生物件進行個別處理，當合成物件的階層數愈多，會使得整個結構變得更複雜，愈難處理底下原生物件的操作。

![](https://i.imgur.com/l8ES04N.png)

---
## Applicability

> 1. 當你想要簡單的呈現出物件之間的樹狀階層關係。
> You want to represent part-whole hierarchies of objects.
> 2. 當你想要讓Client端能夠過一致性的方法處理合成物件架構中的物件。
> You wnat clients to be able to  ignore the difference between compositions of objects and individual objects. Clients will treat all objects in the composite structure uniformly.

---
## Structure

![](https://i.imgur.com/ljmgMiz.png)

>上圖為Composite Pattern的基本結構，此結構主要由Component, Leaf與Composite三個部分組成。Component為Leaf與Composite的共通介面，它定義了一些共通的存取操作，實作基本行為，另外在此也可以宣告Composite遞迴存取Leaf的方法；Leaf為遞迴中最底層的元件，須明確的定義原生的行為與回傳值，否則Composite在遞迴時會因為不明確而進入無窮迴圈；*Composite為Composite Pattern的精隨，它包含了許多Component，可能為Leaf或Composite物件，在此定義了一些管理底下Component的方法，透過遞迴的方式對底下的Component進行操作。Client為透過Component介面操作此Composite結構的物件。*

![](https://i.imgur.com/FJIDv4G.png)
>A typical Composite object structure might look like this

---
## Participants

> - Component
>   1. 描述在 Composite 中物件的interface
>   2. 實作一些共通的部分
>   3. 定義存取、管理其 Child 物件的介面 *(註：其實隨著時間的演進，這一項是否需要在 Component 定義引發了蠻多的討論，現在趨勢是傾向不在 Component 定義管理 Child 物件的介面。上面的 UML 保持當初 Gang of Four 所定義的，讀者也可以試著想想這個問題。)*
>   
> - Leaf (Primitive, Single, Part, Containee)
>   1. 表示在 Composite 中 Leaf 物件，這樣的物件沒有 Child。
>   2. 定義單一特定的物件行為
>   
> - Composite (Group, Whole, Container, Branch)
>   1. 定義有 Child 物件的行為
>   2. 儲存 Child 元件
>   3. 實作 Child 相關的物件行為
>   
> - Client
>   1. 操縱 Compositition 物件透過 Component 所定義的 Interface

---
## Consequences

> 其實 Composite 是一個很好的 Pattern，使用上並沒有太大的副作用。這邊還是做一下簡單的優缺點比較：
>
> - 優點
>   1. 容易加入新類型的 Component
>   2. 對 Client 來說就不需要知道他所處理到的是 Leaf 或著是 Composite
>
> - 缺點
>   1. 難以約束 Compoiste 中 Component 的種類數量

---
## Implementation

 **1. The Base Component**
As a component object we'll define a simple Department interface:
```=
public interface Department {
    void printDepartmentName();
}
```
 **2. Leafs**
For the leaf components, let's define classes for financial and sales departments:
```=
public class FinancialDepartment implements Department {
 
    private Integer id;
    private String name;
 
    public void printDepartmentName() {
        System.out.println(getClass().getSimpleName());
    }
 
    // standard constructor, getters, setters
}
```
The second leaf class, SalesDepartment, is similar:
```=
public class SalesDepartment implements Department {
 
    private Integer id;
    private String name;
 
    public void printDepartmentName() {
        System.out.println(getClass().getSimpleName());
    }
 
    // standard constructor, getters, setters
}
```
Both classes implement the printDepartmentName() method from the base component, where they print the class names for each of them.

Also, as they're leaf classes, they don't contain other Department objects.

Next, let's see a composite class as well.

 **3. The Composite Element**
As a composite class, let's create a HeadDepartment class:
```=
public class HeadDepartment implements Department {
    private Integer id;
    private String name;
 
    private List<Department> childDepartments;
 
    public HeadDepartment(Integer id, String name) {
        this.id = id;
        this.name = name;
        this.childDepartments = new ArrayList<>();
    }
 
    public void printDepartmentName() {
        childDepartments.forEach(Department::printDepartmentName);
    }
 
    public void addDepartment(Department department) {
        childDepartments.add(department);
    }
 
    public void removeDepartment(Department department) {
        childDepartments.remove(department);
    }
}
```
**This is a composite class as it holds a collection of Department components**, as well as methods for adding and removing elements from the list.

The composite printDepartmentName() method is implemented by iterating over the list of leaf elements and invoking the appropriate method for each one.

 **4. Testing**
For testing purposes, let's have a look at a CompositeDemo class:
```=
public class CompositeDemo {
    public static void main(String args[]) {
        Department salesDepartment = new SalesDepartment(
          1, "Sales department");
        Department financialDepartment = new FinancialDepartment(
          2, "Financial department");
 
        HeadDepartment headDepartment = new HeadDepartment(
          3, "Head department");
 
        headDepartment.addDepartment(salesDepartment);
        headDepartment.addDepartment(financialDepartment);
 
        headDepartment.printDepartmentName();
    }
}
```

First, we create two instances for the financial and sales departments. After, we instantiate the head department and add up the previously created instances to it.

Finally, we can test the printDepartmentName() composition method. As we expect, **the output contains the class names of each leaf component:**
```=
SalesDepartment
FinancialDepartment
```

---
## Reference
> 1. http://corrupt003-design-pattern.blogspot.com/2016/08/composite-pattern.html
> 
> 2. https://ithelp.ithome.com.tw/articles/10218208
> 
> 3. http://limitedcode.blogspot.com/2014/10/design-pattern-composite-pattern.html
>
> 4. https://www.baeldung.com/java-composite-pattern
