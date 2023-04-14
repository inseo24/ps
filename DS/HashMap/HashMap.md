### HashMap

- O(1)에 원소 검색, 삽입, 삭제
- key-value, hashing function 을 이용해 key를 배열 인덱스로 변환
- hashing function은 key를 고유 인덱스로 변환하는데 가끔 서로 다른 키가 동일한 인덱스로 해싱되는 충돌이 발생할 수 있음

** 예제 코드는 모두 코틀린

<details>
    <summary> :sparkles: leetcode :sparkles: </summary>

1. [Two Sum](https://leetcode.com/problems/two-sum/)

- 난이도 : 쉬움

<details>
    <summary> 답 </summary>

```kotlin
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        val map = mutableMapOf<Int, Int>()

        nums.mapIndexed { index, num ->
            val complement = target - num
            map[complement]?.let { return intArrayOf(it, index) }
            map[num] = index
        }
        
        throw IllegalArgumentException("No two sum solution")
    }
}


```

</details>

</details>