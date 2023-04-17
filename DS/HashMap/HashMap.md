### HashMap

- O(1)에 원소 검색, 삽입, 삭제
- key-value, hashing function 을 이용해 key를 배열 인덱스로 변환
- hashing function은 key를 고유 인덱스로 변환하는데 가끔 서로 다른 키가 동일한 인덱스로 해싱되는 충돌이 발생할 수 있음

** 예제 코드는 모두 코틀린


<details>
    <summary> :sparkles: leetcode :sparkles: </summary>

1. [Two Sum](https://leetcode.com/problems/two-sum/)

    - 난이도 : 쉬움(Easy)


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

            
2. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
            
    - 난이도 : 중간(Medium)
    - Sliding Window & HashMap
            
        <details>
            <summary> 답 </summary>

        ```kotlin
        import kotlin.math.max

        class Solution {
            fun lengthOfLongestSubstring(s: String): Int {
                var maxLength = 0
                var left = 0
                val charMap = mutableMapOf<Char, Int>()

                for ((right, char) in s.withIndex()) {
                    if (char in charMap && charMap[char]!! >= left) {
                        left = charMap[char]!! + 1
                    }
                    charMap[char] = right
                    maxLength = max(maxLength, right - left + 1)
                }

                return maxLength
            }
        }  
        ```

        </details>
    

3. [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
            
    - 난이도 : 중간(Medium)
            
        <details>
            <summary> 답 </summary>

        ```kotlin
        class Solution {
            fun subarraySum(nums: IntArray, k: Int): Int {
                val sumFrequency = mutableMapOf<Int, Int>().withDefault { 0 }
                sumFrequency[0] = 1

                val (_, count) = nums.fold(Pair(0, 0)) { (prefixSum, count), num ->
                    val newPrefixSum = prefixSum + num
                    val targetSum = newPrefixSum - k
                    val newCount = count + sumFrequency.getValue(targetSum)
                    
                    sumFrequency[newPrefixSum] = sumFrequency.getValue(newPrefixSum) + 1

                    Pair(newPrefixSum, newCount)
                }

                return count
            }
        }
        ```

        </details>

            
3. [Group Anagrams](https://leetcode.com/problems/group-anagrams/)
            
    - 난이도 : 중간(Medium)
            
        <details>
            <summary> 답 </summary>

        ```kotlin
        class Solution {
            fun groupAnagrams(strs: Array<String>): List<List<String>> {
                return strs.groupBy { str -> 
                    str.toCharArray().sorted().joinToString("")
                }.values.toList()
            }
        }
        ```

        </details>
    

</details>
