# ITERATOR
[![hackmd-github-sync-badge](https://hackmd.io/4cnN_jtbTbWJE_3Zo5cZOA/badge)](https://hackmd.io/4cnN_jtbTbWJE_3Zo5cZOA)

## Intent:
>*Iterator 可以用來存取一個聚合器裡的資料，而不用知道聚合器的表示法。*
> Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

---
## Motivation
> 關鍵思想是將訪問和遍歷的責任從聚合器中移出，並將其放入迭代器對像中。

---
## Applicability

> - 對聚合物件（如 Array, Vector, List …）的內部結構一無所知，仍可存取物件。
> to assess an aggregate object's contents without exposing its internal representation.
> - 想用多種方式來巡訪聚合物件時。
> to support multiple traversals of aggregate objects.
> - 想以相同的介面來巡訪各種不同的聚合物件時。
> to provide a uniform interface for traversing different aggregate structures.

---
## Structure

![](https://img-blog.csdnimg.cn/20190918093829406.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01pY2hhZWxpYV9odQ==,size_16,color_FFFFFF,t_70)

---
## Participants

> - Iterator
    - defines an interface for accessing and traversing elements
> - ConcreIterator
    - implements the Iterator interface
    - keeps track of the current position in the traversal of the aggregate
> - Aggregate
    - defines an interface for creating an Iterator object
> - ConcreteAggregate
    - implements the Iterator creating an Iterator object

---
## Consequences

> 1. 對一個聚合器提供多種遍歷方式
    - Complex aggregates may be traversed in many ways.
> 2. Iterator 簡化了聚合器的 interface
> 3. 一個聚合器中可以同時有多個遍歷
    - An iterator keeps track of its own traversal state.

---
## Reference

###### tags: `Design Pattern`
