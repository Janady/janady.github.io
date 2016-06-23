---
layout: post
title: 浅谈排序算法
date:   2016-06-21 13:37:29 +0800
categories: algorithms
---

> 最近对算法比较感兴趣，分治法的拆分、解决与合并，
> 递归的逻辑，动态规划背后的数学表达，
> 深度/广度搜索中的限制条件与边界，
> 哈希表的常数时间的寻址与内存消耗的均衡等。
> 以及后面想聊聊的各种树结构，在构建、插入、搜索的表现。
>
> - 红黑树：一种平衡的搜索二叉树;
> - B树、B+树：更少的树高，经常用于耗时磁盘访问等; 
> - binary indexed tree: 数据与索引巧妙的关联;

下面分享一下对排序的理解，主要考虑算法复杂度以及其常数时间。

- [冒泡排序](#bubble_sort)
- [插入排序](#insertion_sort)
- [合并排序](#merge_sort)
- [堆排序](#heap_sort)
- [快速排序](#quick_sort)

就表现效果而言，[快速排序](#quick_sort)的平均时间消耗最小.
但最坏情况表现不好. 
在STL库中超过一定次数后会切换为[堆排序](#heap_sort)。
[堆排序](#heap_sort)、[合并排序](#merge_sort)
的最坏情况复杂度也为O(nlgn). 

下面说明的序列都以从小到大的方式排序，主要探讨的是算法，也不深究里面范型设计及类型优化等问题。

## <span id = "bubble_sort">冒泡排序</span> ##

# 算法思想 #

对一个序列进行遍历，遍历过程中与前一个元素对比，交换更大的元素到后面。
每次遍历完成最大数据置换到序列末尾，这样一次遍历后序列尾指针前移，直到处理至最后一个元素。

```C++
// 示例区间是前闭后开, [begin, end)
void bubble_sort(iterator begin, iterator end) {
    if (begin == end) return;
    while (begin+1 != end) {
        for (iterator it=begin+1; it!=end; it++) {
            if (*it < *(it-1)) swap(it, it-1);
            --end;
        }
    }
}
```

每次循环内部都进行了比较，伴随着可能的内存移动。
比较操作容易打破处理器的指令流水线, 内循环将花费较多的时钟周期。
这里就不展开汇编代码来分析具体内循环平均占用的指令周期数。

直观的感受是，每个内循环都有操作，判断与移动内存的次数多。相对于插入排序而言，消耗时间更长。

> 
> 时间公式是：`T(n) = T(n-1) + c(n-1); `
> 
> 展开得时间复杂度为O(n<sup>2</sup>)

## <span id = "insertion_sort">插入排序</span> ##

# 算法思想 #

插入排序也是以双层循环的形式进行，
每次遍历插入一个数据到已完成的有序序列中。
一个内循环结束，前端的有序序列增长一次。

```C++
void insertion_sort(iterator begin, iterator end) {
    if (begin == end) return;
    for (iterator i=(begin+1); i!=end; i++) {
        // insert val[i] to sorted array [begin, i).
        T value = *i; // value type T, 此处省去传参或提取类型
        for (iterator it=begin; it<i; ++it) {
            if (*it >= value) {
                /* 从后往前进行内存复制 */
                copy_backward(it, i, i+1);
                *it = value;
                break;
            }
        }
    }
}
```

从结构上看，插入排序与冒泡排序很相似，也有着相同的复杂度O(n<sup>2</sup>)。

但在常数时间上，插入排序优于冒泡排序。可以从`比较次数`和`优化`两个方面分析一下：

>
> **比较次数**
冒泡排序的有序空间在末尾，遍历的每个过程都需要比较。
而插入排序的有序空间在前面，在等概率分布的模型中，
可以节省一半的比较次数。
>
> **优化**
循环中的判断流严重影响循环展开与指令预测，
在插入排序中可以考虑更多的内存移动方式，
减少不必要的分支判断。（此处略过优化细节）

## <span id = "merge_sort">合并排序</span> ##

# 算法思想 #

对于序列[begin, center), [center, end)都已经有序，
那么结合成单一序列也是有序的。
合并排序属于典型分治法的应用，先拆分为子问题，然后进行合并。

```C++
// 示例都以自由寻址访问序列的迭代器说明
void merge_sort(iterator begin, iterator end) {
    if (begin==end || begin+1==end) return;
    // get center of [begin, end)
    iterator center = begin + ((end-begin)>>1);
    merge_sort(begin, center);
    merge_sort(center, end);
    inplace_merge(begin, center, end);
}

/*
 * inplace_merge method
 *
 * 示例代码需要用到额外存储空间, 也可以尝试不用额外空间的解决方案
 * 如此可能需要引入更多指针与判断，以及内存移动来帮助合并，此处略过。
 */
void (iterator begin, iterator center, iterator end) {
    if (begin==center || center==end) return;

    // 为说明思路简单起见，直接分配了center-begin的内存
    // 其他情况自己演化
    T* __buf = new T[center-begin];
    iterator buf = iterator(__buf); // 为说明而用
    copy(begin, center, buf);
    // 有了足够的额外空间，直接合并序列
    iterator f1 = buf, l1 = buf + (center - begin);
    iterator f2 = center, l2 = end;
    iterator output = begin;
    while (f1!=l1 && f2!=l2) { // 两个序列都没走完
        if (*f1 < *f2) {
            *output = *f1;
            ++f1;
        } else {
            *output = *f2;
            ++f2;
        }
        ++output;
    }
    // 将未走完的序列复制到结果中
    copy(f2, l2, copy(f1, l1, output));
    delete [] __buf;
}
```

每次将问题分解为两个n/2的子问题，
然后合并序列，合并操作的复杂度为O(n)。
此外，递归的调用函数，也会占用调用时间和栈空间。调用深度为lgn.

> 
> 时间公式是：`T(n) = 2T(n/2) + cn; `
> 
> 展开得时间复杂度为O(nlgn)。
> 由于每次都是处理有序序列，原有的位置将被频繁改动，内存移动过多，
> 常熟时间相对较大，时间复杂度的推导公式可以看<<算法导论>>。

## <span id = "heap_sort">堆排序</span> ##

# 算法思想 #

堆排序是利用序列容器模拟一个满二叉树，
巧妙的是父子、兄弟等关系都隐含在索引中。
构建的堆的规则是：隐含的二叉树父节点的值不小于其子节点的值。

满足规则后，便有如下特点：

每次操作（插入、移除）的复杂度为树的高度，
隐含的树高不大于lg<sub>2</sub>n。

堆的创建可以视为n次插入，每次插入耗时复杂度O(lgn), 
符合规则的序列长度不断增长，创建树的时间T(create)的复杂度为O(nlgn)。

排序则是每次交换堆顶元素和序列末尾，堆的长度减少。
保证每次交换出去的节点都不小于堆中的数据，而后端已经是一个有序序列。
每次取走堆定后，重新调整堆要经过lg<sub>2</sub>n次比较和内存交换。
因为置换的末尾元素较小，所以每次都需要判断到叶子节点。
这是堆排序平均时间劣与快排的主要因素。

> 
> 时间公式是：`T(n) = T(create) + nlgn; `
> 
> 时间复杂度为O(nlgn)。

## <span id = "quick_sort">快速排序</span> ##

# 算法思想 #

待续...
