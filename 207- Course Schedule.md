# 207. Course Schedule

**# 207. Course Schedule **# 

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (prerequisites == null) return false;

        // step 1: get the indegrees
        Map<Integer, Integer> indegreeMap = indegreeCal(numCourses, prerequisites);

        // step 2: get the start courses
        ArrayList<Integer> startCourseList = getStartCourse(numCourses, indegreeMap);

        // step 3: use BFS to check if we can get all courses
        ArrayList<Integer> courseList = bfs(indegreeMap, startCourseList, prerequisites);
        if (courseList.size() == numCourses) {
            return true;
        }
        return false;
    }

    private Map<Integer, Integer> indegreeCal(int numCourses, int[][] prerequisites) {
        Map<Integer, Integer> indegreeMap = new HashMap<>();

        for (int i = 0; i < numCourses; i++) {
            indegreeMap.put(i, 0);
        }

        for (int i = 0; i < numCourses; i++) {
            for (int[] relation : prerequisites) {
                    if (relation[0] == i) {
                        indegreeMap.put(i, indegreeMap.get(i) + 1);
                    }
            }
        }
        return indegreeMap;
    }

    private static ArrayList<Integer> getStartCourse(int numCourses, Map<Integer, Integer> indegreeMap) {
        ArrayList<Integer> startCourseList = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            if (indegreeMap.get(i) == 0) {
                startCourseList.add(i);
            }
        }
        return startCourseList;
    }

    private ArrayList<Integer> bfs(Map<Integer, Integer> indegreeMap, ArrayList<Integer> startCourseList,
                                   int[][] prerequisites) {
        ArrayList<Integer> courseList = new ArrayList<>();

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < startCourseList.size(); i++) {
            int course = startCourseList.get(i);
            queue.offer(course);
            courseList.add(course);
        }

         while (!queue.isEmpty()) {
            int prerequisite = queue.poll();
            for (int[] relation : prerequisites) {
                if (relation[1] == prerequisite) {
                    int nextCourse = relation[0];
                    int nextCourseIndegree = indegreeMap.get(nextCourse);
                    indegreeMap.put(nextCourse, nextCourseIndegree - 1);
                    if (indegreeMap.get(nextCourse) == 0) {
                        queue.offer(nextCourse);
                        courseList.add(nextCourse);
                    }
                }
            }
        }
        return courseList;
    }
}
