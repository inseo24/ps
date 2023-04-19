### Graph


<details>
  <summary> leetcode </summary>


1. [Course Schedule](https://leetcode.com/problems/course-schedule/submissions/936346639/)

  ```kotlin
  class Solution {
  fun canFinish(numCourses: Int, prerequisites: Array<IntArray>): Boolean {
        val graph = Array<ArrayList<Int>>(numCourses) { ArrayList() }
        val indegrees = IntArray(numCourses)

        for (pre in prerequisites) {
            graph[pre[1]].add(pre[0])
            indegrees[pre[0]]++
        }

        val queue = ArrayDeque<Int>()

        for (i in 0 until numCourses) {
            if (indegrees[i] == 0) {
                queue.add(i)
            }
        }

        while (queue.isNotEmpty()) {
            val course = queue.removeFirst()
            for (nextCourse in graph[course]) {
                indegrees[nextCourse]--
                if (indegrees[nextCourse] == 0) {
                    queue.add(nextCourse)
                }
            }
        }

        return indegrees.all { it == 0 }
    }
  }
  ```

</details>
