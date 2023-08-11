---
title: Shell Sort
tags: Sort
comments: true
---

# 셸 정렬

삽입 정렬 알고리즘을 기반으로 단점이 보완된 알고리즘이다.

셸 정렬은 배열의 요소들을 특정한 간격에 맞추어 부분 리스트로 만들어서 삽입 정렬을 진행하는데 <br>
배열의 요소들을 얼만큼 묶을지 계산하기 위해 gap이라는 값을 사용한다.  <br>
gap을 이용하여 배열을 부분 리스트로 나눈 후 각각 삽입 정렬을 수행한다.

<br>
<hr>

# 셸 정렬 구현

```kotlin
@Test
fun test() {
    val arr = intArrayOf(64, 34, 25, 12, 22, 11, 90)
    println("Original Array: ${arr.joinToString(", ")}")

    shellSort(arr)

    println("Sorted Array: ${arr.joinToString(", ")}")
}

private fun shellSort(arr: IntArray) {
    val n = arr.size
    var gap = n / 2

    while (gap > 0) {
        for (i in gap until n) {
            val temp = arr[i]
            var j = i

            while (j >= gap && arr[j - gap] > temp) {
                arr[j] = arr[j - gap]
                j -= gap
            }

            arr[j] = temp
        }

        gap /= 2
    }
}
```

```
Original Array: 64, 34, 25, 12, 22, 11, 90
Sorted Array: 11, 12, 22, 25, 34, 64, 90
```

