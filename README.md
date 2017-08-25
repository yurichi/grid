"# grid" 


grid-网格布局。
====
它提供了一种机制，设计师可以使用一组可预知标准方案将可用的空间用列或行来布局。
可以精确定位和为元素创建精确的尺寸，应用到网格区域。

参考资料：
complete-guide-grid
css3-grid-layout
grid-layout


几个概念：
网格容器(Grid Containers)、Grid Item
```
<div class="container">
  <div class="item"></div> 
  <div class="item">
          <p class="sub-item"></p>
  </div>
  <div class="item"></div>
</div>
 ``` 
  
网格线(Grid Lines)


网格轨道(Grid Track)
相邻两条网格线之间的空间，就好比表格中行或列。所在在网格中其分为grid column和grid row。每个网格轨道可以设置一个大小，用来控制宽度或高度。


网格单元格(Grid Cell)
网格单元格是指四条网格线之间的空间。所以它是最小的单位，就像表格中的单元格。


网格区域(Grid Area)
任意四条网格线组成的空间，所以他可能包含一个或多个单元格。



*由于网格容器不是块容器，所以有部分属性在网格布局中将会失效


```
Grid Container
display
grid-template-columns
grid-template-rows
grid-template-areas
grid-template
grid-column-gap
grid-row-gap
grid-gap
justify-items
align-items
justify-content
align-content
grid-auto-columns
grid-auto-rows
grid-auto-flow
grid
disaplay
.container { display: grid | inline-grid | subgrid; }
```
###grid 
定义了一个网格容器，它以块级元素的形式显示。
###inline-grid 
定义了一个网格容器，它以内联元素的形式显示。
###subgrid 
如果你的网格容器本身就是一个网格项(即嵌套网格)，你可以使用此属性指定行和列的大小继承于父元素而不是自身指定（次网格）

###grid-template-columns  
###grid-template-rows
定义了一个网格的列数、行数以及网格的大小。
```
.container { 
    grid-template-columns: <track-size> ... | <line-name> <track-size> ...;     
    grid-template-rows: <track-size> ... | <line-name> <track-size> ...;
 }
 ```
定义网格单元的宽高，其单位可以是一个长度(如px、em、rem、vw、vh--基于窗口大小的宽高比例)或百分比，也可以是网格中自由空间的份数(单位为fr)。
定义网格线的名称，它不是必须值。可以一个你选择的任意名字，当没有显示设定时，它的名字以数字表示。

例如：
```
.container {
    grid-template-columns: 40px 50px auto 50px 40px;
    grid-template-rows: 25% 100px auto;
 }
 ```


为了更好地语义化，我们可以给网格线指定一个名字，注意网格线命名时的中括号语法：
```
.container {     
    grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];     
    grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line]; 
}
```
可以使用CSS的repeat()方法来生成多个相同值
```
.box {    
     grid-template-columns: repeat(3, 20px [col-start]) 5%; 
     // grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start] 5%;
 }
 ```

####fr
是一个特殊的单位，它可以类似于设定flex-grow时，给网格容器中的自由空间设置为一个份数，举个例子，下面的例子将把网格容器的每个子项设置为三分之一：
```
.box { 
    grid-template-columns: 1fr 1fr 1fr; 
    }
    ```
也是类似于flex-grow，自由空间是在固定子项确定后开始计算的（这里就如同flex-basis提前给予宽高那样），在下面的例子中自由空间是fr单位的总和但不包括50px：
```
.box {    
   grid-template-columns: 1fr 50px 1fr 1fr;
  }
  ```

####grid-template-areas
grid-template-areas可以配合grid-area定义一个显式的网格区域。
grid-template-areas定义网格区域，然后使用grid-area调用声明好的网格区域名称来放置对应的网格项目。
<grid-area-name>: 使用grid-area属性定义网格区域名称
.: 句点表示一个空单元格
none: 无网格区域被定义
```
<section class="grid">
    <div class="title">title</div>
    <div class="nav">nav</div>
    <div class="main">main</div>
    <div class="aside">aside</div>
    <div class="footer">footer</div>
</section>
```
```
.grid {
    display: grid;
    grid-template-columns: 100px 100px 100px 100px 100px;
    grid-template-rows: 100px 100px 100px 100px;
    grid-template-areas: 'title title title title aside'
                          'nav main main main aside'
                          'nav main main main aside'
                          'footer footer footer footer footer';
    font-size: 30px;
    text-align: center;
}
.title {
    grid-area: title;
    background-color: blue;
}
.nav {
    grid-area: nav;
    background-color: yellow;
}
.main {
    grid-area: main;
    background-color: gray;
}
.aside {
    grid-area: aside;
    background-color: green;
}
.footer {
    grid-area: footer;
    background-color: pink;
}
```
效果如下图：



####grid-column-gap
####grid-row-gap
定义了网格之间的间距。
```
.box {
    grid-column-gap: <line-size>;
    grid-row-gap: <line-size>;
}
```
例如：
```
.box {
    grid-template-columns: 100px 50px 100px;
    grid-template-rows: 80px auto 80px;
    grid-column-gap: 10px;
    grid-row-gap: 15px;
}
```
###justify-items
定义了网格子项的内容和列轴对齐方式，即水平方向上的对齐方式
```
.box {
    justify-items: start | end | center | stretch;
}
```
start代表内容和网格区域的左边对齐。



end代表内容和网格区域的右边对齐。



center代表内容和网格区域的中间对齐。



stretch为默认值，代表填充整个网格区域的宽度。



####align-items
类似于justify-items，align-items定义了网格子项的内容和行轴对齐方式，即垂直方向上的对齐方式。
```
.box {
    align-items: start | end | center | stretch;
}
```
start代表内容和网格区域的上边对齐。


end代表内容和网格区域的下边对齐。



center代表内容和网格区域的中间对齐。


stretch为默认值，代表填充整个网格区域的高度。




###justify-content
网格总大小比它的网格容器的容量小时，导致这个问题的原因可能是所有网格子项都使用了固定值，比如px。justify-content属性定义了网格和网格容器列轴对齐方式（和align-content相反，它是和行轴对齐）。
```
.box {
    justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```
start代表网格在网格容器左边对齐。


end代表网格在网格容器右边对齐。


center代表网格在网格容器中间对齐。


stretch改变网格子项的容量让其填充整个网格容器宽度。


space-around代表在每个网格子项中间放置均等的空间，在始末两端只有一半大小。


space-between代表在每个网格子项中间放置均等的空间，在始末两端没有空间。


space-evenly代表在每个网格子项中间放置均等的空间，包括始末两端。



align-content
类似于justify-content，align-content属性定义了网格和网格容器行轴对齐方式。
```
.box {
    align-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```
start代表网格在网格容器上边对齐。
end代表网格在网格容器下边对齐。
center代表网格在网格容器中间对齐。
stretch改变网格子项的容量让其填充整个网格容器高度。
space-around代表在每个网格子项中间放置均等的空间，在始末两端只有一半大小。
space-between代表在每个网格子项中间放置均等的空间，在始末两端没有空间。
space-evenly代表在每个网格子项中间放置均等的空间，包括始末两端。

grid-auto-columns
grid-auto-rows
grid-template-columns、grid-template-rows和grid-template-areas三个属性可以定义一个显式的网格，确定网格的轨道以及网格行数和列数的明确数量。 
grid-auto-columns与grid-auto-rows可以指定隐式网格。
```
.box {
    grid-auto-columns: <track-size> ...;
    grid-auto-rows: <track-size> ...;
}
```

例：
```
.container {
    grid-template-columns: 60px 60px;
    grid-template-rows: 90px 90px
}  
.item-a {
    grid-column: 1 / 2;
    grid-row: 2 / 3;
}
.item-b {
    grid-column: 5 / 6;
    grid-row: 2 / 3;
}
```


grid-auto-flow
其实grid布局自身具有的自动布局算法会将网格子项自动放置起来，而grid-auto-flow属性控制自动布局算法如何工作。（未指定固定位置模块的排布方式）
```
.box {
    grid-auto-flow: row | column | row dense | column dense
}
```
row 默认值，
代表自动布局算法在每一行中依次填充，只有必要时才会添加新行。



column
代表自动布局算法在每一列中依次填充，只有必要时才会添加新行。



dense
代表告诉自动布局算法如果更小的子项出现时尝试在网格中填补空位。

```
#grid {
        height: 200px;
        width: 200px;
        display: grid;
        grid-gap: 10px;
        grid-template: repeat(4, 1fr) / repeat(2, 1fr);
        grid-auto-flow: column  dense;
}
#item1 {
        background-color: lime;
        grid-row-start: 3;
}
```
dense等同于row dense

---尽量不要将这个属性设置为dense，因为它可能让我们的页面布局产生混乱




grid为以下属性的合并写法：
grid-template-rows，grid-template-columns，grid-template-areas，grid-auto-rows，grid-auto-columns，grid-auto-flow。
它也可以设置grid-column-gap和grid-row-gap。
```
.box {
    grid: none | <grid-template-rows> / <grid-template-columns> | <grid-auto-flow> [<grid-auto-rows> [/ <grid-auto-columns>]];
}
```


Grid Items
grid-column-start
grid-column-end
grid-row-start
grid-row-end
grid-column
grid-row
grid-area
justify-self
align-self
grid-column-start
定义了网格项目垂直方向的开始位置网格线。
grid-column-end
定义了网格项目垂直方向的结束位置网格线。
grid-row-start
定义了网格项目水平方向的开始位置网格线。
grid-row-end
定义了网格项目水平方向的结束位置网格线。

```
.item {     
    grid-column-start: <number> | <name> | span <number> | span <name> | auto     
    grid-column-end: <number> | <name> | span <number> | span <name> | auto     
    grid-row-start: <number> | <name> | span <number> | span <name> | auto     
    grid-row-end: <number> | <name> | span <number> | span <name> | auto 
}
```
<line>表示网格线名称。
span <number>表示子项将跨越指定数字数目的网格轨迹。
span <name>表示子项将跨越到指定名字之前的网格线。
auto表示自动布局，自动跨越或者默认跨越一个。

```
.item-a {
    grid-column-start: 2;
    grid-column-end: five;
    grid-row-start: row1-start;
    grid-row-end: 3;
}

.item-b {
    grid-column-start: 1;
    grid-column-end: span col4-start;
    grid-row-start: 2
    grid-row-end: span 2
}
```
注：如果没有显式设置grid-column-end/grid-row-end，网格子项将默认跨越一个网格单元。此外，网格子项可以互相重叠，你可以使用z-index来控制他们的层叠顺序。

grid-column
grid-column-start + grid-column-end
grid-row
grid-row-start + grid-row-end

```
.item {
    grid-column: <start-line> / <end-line> | <start-line> / span <value>;
    grid-row: <start-line> / <end-line> | <start-line> / span <value>;
}

.item-c {
    grid-column: 3 / span 2;
    grid-row: third-line / 4;
}
```


grid-area
grid-area调用grid-template-areas属性创建的模板。
grid-row-start+ grid-column-start + grid-row-end+ grid-column-end
```
.item {
    grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
}
 ```
justify-self
justify-self定义了该网格单元的内容和列轴对齐方式，即水平方向上的对齐方式。

```
.box {
    justify-self: start | end | center | stretch;
}
```
start代表该网格单元和网格区域的左边对齐。
end代表该网格单元和网格区域的右边对齐。
center代表该网格单元和网格区域的中间对齐。
stretch为默认值，代表填充整个网格区域的宽度。
align-self
类似于justify-self，align-self定义了该网格单元的内容和水平轴对齐方式，即垂直方向上的对齐方式。

```
.box {     
    align-self: start | end | center | stretch; 
} 
```
start代表该网格单元和网格区域的上边对齐。
end代表该网格单元和网格区域的下边对齐。
center代表该网格单元和网格区域的中间对齐。
stretch为默认值，代表填充整个网格区域的高度。




