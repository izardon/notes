# VISITOR

[![hackmd-github-sync-badge](https://hackmd.io/4cnN_jtbTbWJE_3Zo5cZOA/badge)](https://hackmd.io/4cnN_jtbTbWJE_3Zo5cZOA)

## Intent:
> 表示一個作用於某物件結構中的各元素之操作。訪問者讓你可以定義新操作，而無須更改其所操作元素的類。
> Represent an operation to be performed on elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

---
## Applicability

> - 元素的個數是固定時(穩定的資料結構)。
>   - 缺點是資料結構(元素)的增加變得更為困難了。
> 
> - 將處理和資料結構兩者分離開來。
> - 增加操作就等於是增加新的Visitor。


---
## Structure

![](https://i.imgur.com/ERCESB8.png)

![](https://i.imgur.com/rYRJKk9.png)


---
## Participants

> - Visitor
    - 為每一個具體的元素(Element)類別宣告一個Visit操作。
> - ConcreteVisitor
    - 需要對每一個元素實作具體的Visit行為。
> - Element
    - 以訪問者為參數的Accept操作。
> - ConcreteElement
    - 需要時做Accept方法，通常是指接受存取的方法的實作。
> - ObjectStructure
    - 能枚舉他的元素，提供給Visitor訪問的介面。(may be a Composite)

---
## Consequences

> 1. 增加新操作容易
> Visitor makes adding new operations easy.
> 2. 操作有關的程式碼都集中起來
> A visitor gathers related operations and separates unrelated ones.
> 3. 新增或修改元件類別困難
> Adding new ConcreteElement classes is hard.
> 4. 搭配使用合成模式，可以尋訪不同結構的元素
> Visiting across class hierarchies.
> 5. 狀態累積
> Accumulating state.
> 6. 破壞類別的封裝
> Breaking encapsulation.

---
## Reference
> - https://ithelp.ithome.com.tw/articles/10208766
> - http://corrupt003-design-pattern.blogspot.com/2017/02/visitor-pattern.html
###### tags: `Design Pattern`
