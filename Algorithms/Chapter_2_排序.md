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
+ 特点：性能无法估计、代码量很小、不需要使用额外的内存空间
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

+ 希尔排序比插入排序和选择排序要快的多，数组越大，优势越大

## 归并排序

+ 归并：将两个有序的数组归并成一个更大的有序数组
+ 归并排序：递归排序，要将一个数组排序，首先将它分成两半分别排序，然后将结果归并起来
+ 性质：
    1. 优点：能够保证任意长度为N的数组排序所需时间和NlogN成正比
    2. 缺点：所需的额外空间和N成正比

### 原地归并的抽象方法

+ 核心代码：（merge算法）

    ```java
    public static void merge(Comparable[] a, int low, int middle, int high) {
        // 将a[low ... middle] 和 a[middie + 1 ... high] 归并起来
        int i = low;
        int j = middle + 1;

        for (int k = low; k <= high; k++) // 将a[low ... high]复制到aux[low ... high]辅助数组中
            aux[k] = a[k];

        for (int k = low; k <= high; k++) { // 归并回到a[low ... high]
            if      (i > middle)            a[k] = aux[j++]; //左半边用尽（取右半边的元素）
            else if (j > high)              a[k] = aux[i++]; //右半边用尽（取左半边的元素）
            else if less(aux[j], aux[i])    a[k] = aux[j++]; //右半边的当前元素小于左半边的当前元素（取右半边的元素）
            else                            a[k] = aux[i++]; //右半边的当前元素大于左半边的当前元素（取左半边的元素）
        }
    }
    ```

### 自顶向下的归并排序

+ 性质：
    1. 对于长度为N的任意数组，自顶向下的归并 **排序** 需要次数：
        $$ \frac{1}{2}NlgN 至 NlgN$$
    2. 对于长度为N的任意数组，自顶向下的归并排序最多需要 **访问数组** 次数：6NlgN

+ 核心代码：（sort算法）

    ```java
    private static Comparable[] aux; //辅助数组
    public static void sort(Comparable[] a) {
        aux = new Comparable[a.length]; //一次性分配空间
        sort(a, 0, a.length - 1);
    }
    private static void sort(Comparable[] a, int low, int high) {
        if (hi <= low) return; //排序结束
        int middle = low + (high - low) / 2; //找中点
        sort(a, low, mid); //左半边排序
        sort(a, middle, high); //右半边排序
        merge(a, low, middle, high); //归并两个数组
    }
    ```
