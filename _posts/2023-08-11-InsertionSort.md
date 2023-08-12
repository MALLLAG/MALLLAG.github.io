---
title: Insertion Sort
tags: Sort
comments: true
---

# 삽입 정렬

배열을 기준으로 두 번째 요소인 첫 번째 인덱스부터 자신의 앞 요소인 배열의 첫 번째 요소까지 비교하여 정렬될 위치를 찾아 삽입하는 알고리즘이다. <br>
오름차순으로 정렬된 배열을 내림차순으로 정렬하는 최악의 경우 O(n^2)의 시간 복잡도를 가진다. <br>
버블 정렬과 선택 정렬에 비해 최선의 경우 O(n) 시간 복잡도를 가지므로 두 정렬보다 효율이 좋다.

![1](https://github.com/MALLLAG/MALLLAG.github.io/assets/87420630/d78a5ad7-8443-4edb-80b4-77ffd5127568)

<br>
<hr>

# 삽입 정렬 구현

```kotlin
@Test
fun test() {
    val arr = intArrayOf(64, 34, 25, 12, 22, 11, 90)
    println("Original Array: ${arr.joinToString(", ")}")

    insertionSort(arr)

    println("Sorted Array: ${arr.joinToString(", ")}")
}

private fun insertionSort(arr: IntArray) {
    val n = arr.size
    for (i in 1 until n) {
        val target = arr[i]
        var j = i - 1

        while (j >= 0 && arr[j] > target) {
            arr[j + 1] = arr[j]
            j--
        }

        arr[j + 1] = target
    }
}
```

```
Original Array: 64, 34, 25, 12, 22, 11, 90
Sorted Array: 11, 12, 22, 25, 34, 64, 90
```
