# COMPOSITE

[![hackmd-github-sync-badge](https://hackmd.io/4cnN_jtbTbWJE_3Zo5cZOA/badge)](https://hackmd.io/4cnN_jtbTbWJE_3Zo5cZOA)

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
## Reference
> 1. http://corrupt003-design-pattern.blogspot.com/2016/08/composite-pattern.html
> 
> 2. https://ithelp.ithome.com.tw/articles/10218208
> 
> 3. http://limitedcode.blogspot.com/2014/10/design-pattern-composite-pattern.html
>
> 4. https://www.baeldung.com/java-composite-pattern

###### tags: `Design Pattern`
