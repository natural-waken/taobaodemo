# grid布局

> 三大布局方式
>
> - 传统布局方式————利用position display float 布局  兼容性最好 效率低
> - flex 布局————效率高
> - grid布局————强大
>
> nh
>
> nh



## 基本概念

> 什么是grid布局

flex 布局是**轴线布局**  只能指定“项目”针对轴线的位置   可以看作是一维布局   

grid布局则是将容器划分成**“行”和“列”**   产生单元格  可以看作是二维布局   grid布局远比flex布局强大

> 像一个格子一个格子排列  更加灵活强大

> 容器————有容器属性   包裹的容器
>
> 项目————有项目属性   里面的子元素

![image-20230310205900146](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310205900146.png)



## 容器属性

> 1. grid-template-columns
> 2. grid-template-rows
> 3. grid-row-gap
> 4. grid-column-gap
> 5. grid-gap (3和4的简写)
> 6. grid-template-areas
> 7. grid-auto-flow
> 8. justify-items
> 9. align-items
> 10. place-items(8和9的简写)
> 11. justify-content
> 12. align-content
> 13. place-content(11和12的简写)
> 14. grid-auto-columns
> 15. grid-auto-rows



#### 一、grid-template

> 你想要多少行或者列   就填写相应属性值的个数  不填写  自动分配
>
> 1. grid-template-columns
>
> 2. grid-template-rows
>
>    



![image-20230310194206412](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310194206412.png)

```html 
.main {
    display: grid;
    width: 600px;
    height: 600px;
    border: 10px solid skyblue;

    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 100px 100px 100px 100px;
    }

<div class="main">
        <div class="item item-1">1</div>
        <div class="item item-2">2</div>
        <div class="item item-3">3</div>
        <div class="item item-4">4</div>
        <div class="item item-5">5</div>
        <div class="item item-6">6</div>
        <div class="item item-7">7</div>
        <div class="item item-8">8</div>
        <div class="item item-9">9</div>
        <div class="item item-10">10</div>
    </div>
```

设置结果出来如上图



##### 1.repeat() 

> 第一个参数是重复的次数     第二个参数是所要重复的值

```html
grid-template-columns: 100px 100px 100px;
// 等价于
grid-template-columns: repeat(3, 100px);
```



##### 2.auto-fill

> 有时  单元格的大小是固定的  但是容器的大小不确定   这属性就会**自动填充**

```html
grid-template-columns: repeat(auto-fill, 100px);
// 按 每个 100px  排列 填满几个是几个
```

![image-20230310201643262](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310201643262.png)



##### 3.fr

> 为了方便表示比例关系  网格布局提供了 **fr 关键字**  fraction  "片段"
>
> 

```html
grid-template-columns: repeat(3,1fr);
//  等价于
grid-template-columns: 1fr 1fr 1fr;
// 把列平均分成三列
```

![image-20230310200909406](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310200909406.png)



```html
grid-template-columns: 1fr 2fr 3fr;
// 第一个占一份 第二个占两份 第三个占三份
```

![image-20230310202139908](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310202139908.png)



##### 4.minmax() 

> 函数产生一个长度范围  表示这个长度在范围中  他接受两个参数  分别为最大值和最小值
>
> 

```html
grid-template-columns: 1fr minmax(550px,1fr);
// 分为两列 一列是 1fr 另一列是最小宽度是 550px 最大宽度是 1fr
```

![image-20230310203449678](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310203449678.png)



##### 5.auto

> 表示由浏览器自身决定长度

```html
grid-template-columns: 100px auto 100px;
// 分为三列 第一列是100px 第二列是自动 第三列是100px
```

![image-20230310203750075](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310203750075.png)



##### 6.网格线

> 可以用方括号定义网格线名称  方便以后引用

```html
grid-template-columns: [c1] 100px [c2] 100px [c3] 100px [c4];
```



#### 二、grid-row-gap / grid-column-gap

> 一句话解释就是 item（项目）相互之间的距离
>
> **tip:** 根据最新标准  上面三个属性名的 gird- 前缀已经删除  写成 **column-gap**  **row-gap**   grid-gap 写成 **gap**
>
> 

```html
.main {
    display: grid;
    width: 600px;
    height: 600px;
    border: 10px solid skyblue;

	/* 三列 四条线 */
	grid-template-columns: [c1] 100px [c2] 100px [c3] 100px [c4];
	grid-template-rows: 100px 100px 100px 100px;

	// 行间距  每一行和每一行
	row-gap: 20px;
	// 列间距  每一列和每一列
	column-gap: 20px;
	// 综合写法
	gap:20px 20px;
}
```

![image-20230310210658739](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310210658739.png)



#### 三、grid-template-areas

> 一个区域由单个或多个单元格组成  由你决定（具体使用  需要在项目属性里面设置）



![image-20230310211255684](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310211255684.png)

如上图第一种方式：每个都是不同的区域

​			第二种方式：a a a 都是同一块区域 b b b 是另一块区域  c c c 是另一块区域

​			第三种方式：a 是一块区域 . 表示这块数据不是区域  不想被划分为区域  c 是另一块区域



#### 四、grid-auto-flow

> 划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格。默认的放置顺序是“**先行后列**"  即先填满第一行，再开始放入第二行 (**就是子素的排放顺序**)
>
> 

```html
grid-auto-flow: row;
// 这个就是先排列行  行满了再排列  
grid-auto-flow: column;
// 这个是先排列 再排行
```



> 相关信息
>
> 当出现图中所示情况时  此时2 在第一行放不下 放在第二行 3 只能也放在第二行  这样空间利用率不是很大  所以有了这个属性  可以成为图二中的情况
>
> 加第二个属性即可 grid-auto-flow: row dense;

![image-20230310212201068](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310212201068.png)



#### 五、justify-items      align-items 

> 设置单元格内容的水平和垂直对齐方式
>
> justify-items 水平方向 align-items 垂直方向



![image-20230310212847715](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310212847715.png)

![image-20230310215340522](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310215340522.png)

```html
justify-items: center;
align-items: center;
// 产生下图原因是 每一个子元素没有设置宽高  所以居中以文字  前面之所以撑开是背景默认填充了

// 组合写法是
place-items: center center;
```

![image-20230310214359166](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310214359166.png)





#### 六、justify-content   align-content

> 这个是设置**整个内容区域**的水平垂直对齐方式
>
> 上面那个是每个子元素的对齐方式
>
> 对齐方式和flex布局类似 属性

![image-20230310214805867](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310214805867.png)

```html
justify-content: center;
align-content: center;
```

![image-20230310215718750](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310215718750.png)

![image-20230310215950309](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310215950309.png)



#### 七、grid-auto-columns grid-auto-rows

> 用来设置多出来的项目宽和高
>
> 

![image-20230310220405111](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310220405111.png)

```html
grid-template-columns: 100px 100px 100px;
grid-template-rows: 100px 100px 100px;
// 这里只设置了三乘三个区域  而实际上又是个盒子
// 所以这个属性就是用来设置多出来的盒子
grid-auto-rows: 50px;
```



## 项目属性

> 1. grid-column-start
> 2. grid-column-end
> 3. grid-row-start
> 4. grid-row-end
> 5. grid-column(1和2的简写形式)
> 6. grid-row (3和4的简写形式)
> 7. grid-area
> 8. justify-self
> 9. align-self
> 10. place-self (8和9的简写形式)



#### 一、grid-column-start / end  grid-row-start /  end

> 一句话解释  用来指定item 的具体位置 根据在哪跟网格线
>
> grid-column-start / end 是从列的角度开始 数列找网格线
>
> grid-row-start /  end 是从行的角度开始 数列找网格线

![image-20230310222129805](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310222129805.png)

```html
grid-column-start: 1;
grid-column-end: 3;
// 简写
grid-column: 1 / 3;
```

![image-20230310222926495](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310222926495.png)



![image-20230310223149813](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310223149813.png)



> 还有一种写法

```html
grid-column-start: span 2;
```

![image-20230310223609436](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310223609436.png)



#### 二、grid-area

> 在父元素中选择子元素的区域

```html
grid-template-areas: 'a a a' 'b b b' 'c c c';
// 上面这个是给父元素添加
grid-area: b;
// 这个是给子元素添加
```

![image-20230310224034140](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230310224034140.png)



#### 三、justify-self  align-self

> 子元素自身设置对齐方式
>

![image-20230311181320393](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230311181320393.png)



```html
.item2 {
	justify-self: center;
}
```

![image-20230311181505548](C:\Users\86182\AppData\Roaming\Typora\typora-user-images\image-20230311181505548.png)





















