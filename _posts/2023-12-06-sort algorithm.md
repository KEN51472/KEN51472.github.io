---
layout: detail
type : 2
keyword :     
title: sort algorithm
description: 
---

## 冒泡排序

冒泡排序（Bubble Sort）: 
重复地遍历要排序的序列，一次比较两个相邻的元素，如果它们的顺序错误就将它们交换。遍历的过程会把最大的元素“浮”到最后，因此称为冒泡排序。
```c
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if (arr[j] > arr[j+1]) {
                std::swap(arr[j], arr[j+1]);
            }
        }
    }
}
```
冒泡排序的时间复杂度为 O(n^2)，空间复杂度为 O(1)。它的优点是实现简单，缺点是效率较低，不适用于大规模数据的排序。

## 归并排序

归并排序（Merge Sort）: 
一种分治算法，它将待排序的序列分成两个子序列，分别进行排序，然后将两个已排序的子序列合并成一个有序序列。
```c
// 合并两个已排序的子数组
void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1; // 左子数组的大小
    int n2 = r - m;     // 右子数组的大小

    // 创建临时数组存储左右子数组
    int L[n1], R[n2];
    for (int i = 0; i < n1; i++) {
        L[i] = arr[l + i]; // 将数据复制到临时数组中
    }
    for (int j = 0; j < n2; j++) {
        R[j] = arr[m + 1 + j]; // 将数据复制到临时数组中
    }

    // 合并左右子数组
    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i]; // 从临时数组中取出较小的元素放入原数组中
            i++;
        } else {
            arr[k] = R[j]; // 从临时数组中取出较小的元素放入原数组中
            j++;
        }
        k++;
    }

    // 将剩余的元素复制到数组中
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// 归并排序
void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2; // 计算中间元素的索引
        // 递归排序左右子数组
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        // 合并已排序的子数组
        merge(arr, l, m, r);
    }
}

```

归并排序的时间复杂度为 O(nlogn)，空间复杂度为 O(n)。它的优点是稳定且高效，适用于大规模数据的排序。


## 快速排序
快速排序（Quick Sort）: 
一种分治算法，选择一个基准元素，将序列分成两部分，小于基准元素的放在左边，大于基准元素的放在右边，然后对左右两部分分别进行排序。
```c
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] < pivot) {
            i++;
            std::swap(arr[i], arr[j]);
        }
    }

    std::swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

```
快速排序的时间复杂度为 O(nlogn)，空间复杂度取决于递归调用的深度。它的优点是效率高，适用于大规模数据的排序，但在最坏情况下可能会退化为 O(n^2)。

冒泡排序适用于简单的排序任务，但效率较低；归并排序适用于大规模数据的排序，且稳定高效；快速排序也适用于大规模数据的排序，但需要注意最坏情况下的性能。