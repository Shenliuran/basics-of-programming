# 第二章 排序

## 初级排序算法

### 选择排序

+ 时间复杂度：
    $$ \Theta(n^2) $$
+ 核心算法：

    ```java
    public static void sort(Comparable[] a) {
        for (int i = 0; i < a.length; i++) {
            int min = i;
            for (int j = i + 1; j < a.length; j++)
                if (less(a[j], a[min])) min = j;
            exch(a, i, min);
        }
    }
    ```

### 插入排序

+ 插入排序所需的时间却决于输入元素的初始顺序
+ 最好的情况下，时间时间复杂度为：
    $$ \Theta(n) 或者 \Theta(0) $$
+ 最坏情况下,时间复杂度为:
    $$ \Theta(n^2) $$
+ 核心算法:

    ```java
    public static void sort(Comparable[] a) {
        for (int i = 1; i < a.length; i++) {
            for (int j = i; j > 0 && less(a[j], a[j - 1]; j--)) //每次都是相邻的两个元素进行比较
                exch(a, j, j - 1);
        }
    }
    ```

### 希尔排序

+ 基于插入排序
+ 思想: 使数组中任意间隔为h的元素都是有序的,这样的数组被称为h有序数组
+ 高效的原因: 权衡了子数组的规模和有序性. 排序之初,各个子数组都很短,排序之后子数组都是部分有序的,这种情况很适合插入排序
+ 性能无法估计
+ 核心算法:

    ```java
    public static void sort(Comparable[] a) {
        while (h < a.lenght / 3)
            h = 3 * h + 1;
        while (h >= 1) {
            //将数组变成h有序
            for (int i = h; j < a.length; i++) {
                for (int j = i; j >= h && less(a[j], a[j - h]); j -= h)
                    exch(a, j, j - h);
            }
        }
        h = h / 3; //将子数组缩减
    }
    ```

## 归并排序
