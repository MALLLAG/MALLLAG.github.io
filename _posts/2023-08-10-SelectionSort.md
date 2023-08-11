---
title: Selection Sort
tags: Sort
comments: true
---

# 선택 정렬

주어진 배열에서 순회를 할 때마다 최솟값 및 최댓값을 찾아서 배열의 앞 쪽으로 정렬하는 알고리즘이다. <br>
최악의 경우에는 버블 정렬과 동일하게 O(n^2)의 시간 복잡도를 가진다.

1. 배열에서 최솟값을 찾는다.
2. 1의 값을 배열의 맨 앞과 교체한다.
3. 교체한 자리를 제외하고 정렬할 개수가 1개만 남을때까지 반복한다.

![2](https://github.com/MALLLAG/MALLLAG.github.io/assets/87420630/de8d356b-efe8-4eee-ac94-61d67ef05281)

<br>
<hr>


# 선택 정렬 구현

```kotlin
@Test
fun test() {
    val arr = intArrayOf(64, 25, 12, 22, 11, 11)
    println("Original Array: ${arr.joinToString(", ")}")

    selectionSort(arr)

    println("Sorted Array: ${arr.joinToString(", ")}")
}

private fun selectionSort(arr: IntArray) {
    val n = arr.size
    for (i in 0 until n - 1) {
        var minIndex = i
        for (j in i + 1 until n) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j
            }
        }

        val temp = arr[i]
        arr[i] = arr[minIndex]
        arr[minIndex] = temp
    }
}
```

```
Original Array: 64, 25, 12, 22, 11, 11
Sorted Array: 11, 11, 12, 22, 25, 64
```
