---
title: Bubble Sort
tags: Sort
comments: true
---

# 버블 정렬

인접한 두 요소의 값을 비교하여 대소관계에 따라 서로 자리를 교체한다. <br>
최악의 경우 [1,2,3,4,5]의 배열을 역순으로 정렬하면 모든 요소의 자리를 교체하기 때문에 O(n^2)의 시간복잡도를 가진다. <br>
속도가 매우 느린 알고리즘이지만 구현이 간단하여 데이터가 적은 곳에서 주로 사용한다.

<br>
<hr>

# 버블 정렬 구현

```kotlin
@Test
fun test() {
    val arr = intArrayOf(64, 34, 25, 12, 22, 11, 90)
    println("Original Array: ${arr.joinToString(", ")}")

    bubbleSort(arr)

    println("Sorted Array: ${arr.joinToString(", ")}")
}

private fun bubbleSort(arr: IntArray) {
    val n = arr.size
    for (i in 0 until n - 1) {
        for (j in 0 until n - i - 1) {
            if (arr[j] > arr[j + 1]) {
                val temp = arr[j]
                arr[j] = arr[j + 1]
                arr[j + 1] = temp
            }
        }
    }
}
```

```
Original Array: 64, 34, 25, 12, 22, 11, 90
Sorted Array: 11, 12, 22, 25, 34, 64, 90
```

