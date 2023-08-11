---
title: Merge Sort
tags: Sort
comments: true
---

# 병합 정렬

병합 정렬은 분할 정복 전략의 한 종류이다. *분할 정복이란, 어떤 문제를 작은 단위의 문제로 나누어 해결하고 결과를 다시 하나의 문제로 해결하는 것*

분할 정복을 토대로 병합 정렬은 배열을 균등한 크기로 분할할 수 없을 때까지 분할하고, 두 부분 리스트를 정렬과 동시에 병합하여 정렬된 결과를 구하는 방법이다. <br>
병합 정렬은 최선 및 최악의 경우 모두 O(nlogn) 시간 복잡도를 가진다.

병합하는 과정에서 분할된 부분 리스트를 정렬하기 위해 두 부분 리스트를 합한 크기만큼 임시로 담을 배열을 <br>
메모리에 할당하기 때문에 다른 정렬 알고리즘에 비해 메모리 사용량이 높다.

<br>
<hr>

# 병합 정렬 구현

```kotlin
@Test
fun test() {
    val arr = intArrayOf(64, 34, 25, 12, 22, 11)
    println("Original Array: ${arr.joinToString(", ")}")

    mergeSort(arr)

    println("Sorted Array: ${arr.joinToString(", ")}")
}

private fun mergeSort(arr: IntArray) {
    // 배열의 크기가 1 이하면 이미 정렬된 상태이므로 리턴
    if (arr.size <= 1) return

    // 배열을 중간을 기준으로 두 부분으로 분할
    val mid = arr.size / 2
    val left = arr.copyOfRange(0, mid)
    val right = arr.copyOfRange(mid, arr.size)

    // 각 부분 배열에 대해 재귀적으로 mergeSort 함수를 호출
    mergeSort(left)
    mergeSort(right)

    // 분할된 부분 배열을 병합
    merge(arr, left, right)
}

private fun merge(arr: IntArray, left: IntArray, right: IntArray) {
    var i = 0 // 왼쪽 부분 배열의 인덱스
    var j = 0 // 오른쪽 부분 배열의 인덱스
    var k = 0 // 합쳐질 배열 arr의 인덱스

    // 왼쪽과 오른쪽 부분 배열을 비교하면서 정렬된 배열 arr에 병합
    while (i < left.size && j < right.size) {
        if (left[i] < right[j]) {
            arr[k++] = left[i++]
        } else {
            arr[k++] = right[j++]
        }
    }

    // 남아있는 원소들을 모두 병합
    while (i < left.size) {
        arr[k++] = left[i++]
    }

    while (j < right.size) {
        arr[k++] = right[j++]
    }
}
```

```
Original Array: 64, 34, 25, 12, 22, 11
Sorted Array: 11, 12, 22, 25, 34, 64
```
