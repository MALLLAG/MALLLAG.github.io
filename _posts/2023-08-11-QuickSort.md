---
title: Quick Sort
tags: Sort
comments: true
---

# 퀵 정렬

퀵 정렬은 병합 정렬과 같은 분할 정복 전략의 종류이다. <br>
병합 정렬에선 분할 과정이 오로지 배열을 분할하는 데만 집중했다면, 퀵 정렬은 분할 과정에서 정렬이 함께 이루어진다.

시간 복잡도는 최악의 경우 O(n^2)이지만 평균 수행 시간은 병합 정렬과 같은 O(nlogn)이다. <br>
퀵 정렬은 임시 배열을 사용하지 않기 때문에 메모리 사용량이 병합 정렬보다 낮다.

퀵 정렬에서 필수 요소인 피벗은 정렬 시에 기준이 될 값이다. <br>
[26, 10, 35, 19, 7, 3, 12]의 배열에서 모든 요소가 피벗이 될 수 있으며, 일반적으로 배열의 첫 번째 요소, 중간 요소, 마지막 요소를 사용한다.

피벗을 기준으로 좌측은 피벗보다 작은 값으로 이루어져야 하고 우측은 피벗보다 큰 값으로 이루어져야 한다.

<br>
<hr>

# 퀵 정렬 구현

```kotlin
@Test
fun test() {
    val arr = intArrayOf(64, 34, 25, 12, 22, 11, 90)
    println("Original Array: ${arr.joinToString(", ")}")

    quickSort(arr, 0, arr.size - 1)

    println("Sorted Array: ${arr.joinToString(", ")}")
}

private fun quickSort(arr: IntArray, left: Int, right: Int) {
    if (left >= right) {
        return
    }

    var i = left
    var j = right

    // 배열의 가운데 요소를 pivot으로 설정
    val pivot = arr[(left + right) / 2]

    while (i < j) {
        // pivot의 좌측은 pivot보다 작은 값만 두고 큰 값을 찾는다
        while (arr[i] < pivot) {
            i++
        }

        // pivot의 우측은 pivot보다 큰 값만 두고 작은 값을 찾는다
        while (arr[j] > pivot) {
            j--
        }

        // i, j가 교차되면 분할을 멈춘다
        if (i >= j) {
            break
        }

        // i, j가 pivot과 같으면 i만 오른쪽으로 한 칸 이동
        if (arr[i] == pivot && arr[j] == pivot) {
            i++
            continue
        }

        val temp = arr[i]
        arr[i] = arr[j]
        arr[j] = temp

        quickSort(arr, left, i - 1)
        quickSort(arr, i + 1, right)
    }
}
```

```
Original Array: 64, 34, 25, 12, 22, 11, 90
Sorted Array: 11, 12, 22, 25, 34, 64, 90
```


