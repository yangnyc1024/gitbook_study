# Topological Order--- course schedule

## Question

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

* For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.



## Classification& Assumption

* Graph Representation
  * Vertex: course
  * Edge: dependency course

## High Level

* Problem definition
  * find a topological order in a directed graph
* choose traversal algorithm
  * dfs2 & bfs

## Middle Level

&#x20;Method 1

* graph representation:&#x20;
  * vertex: course, int\[]
  * edge: dependency course, Set\<Integer>
* visited:&#x20;
  * enum State



Method 3

* graph representation:
  * wrapped class
    * visited?
      * enum State? or not
    * set of preCourse
    * set of nextCourse

## TC & SC

* TC: O(|V|+ |E|)&#x20;
* SC: O(|V|)





Code: Method 3:

```java
class Solution {
    class Course {
        int courseNumber;
        Set<Course> prevCourse;
        Set<Course> nextCourse;
        boolean visited;
        boolean visiting;
        public Course(int course) {
            this.courseNumber = course;
            this.prevCourse = new HashSet<>();
            this.nextCourse = new HashSet<>();
            this.visited = false;
            this.visiting = false;
        }
        @Override
        public int hashCode(){
            int hashCode = this.courseNumber  * 31 + 31;
            return hashCode;
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (obj == null) return false;
            if (this.getClass() != obj.getClass()) {
                return false;
            }
            Course that = (Course) obj;
            return this.courseNumber == that.courseNumber;
        }

    }
    class ReturnType{
        boolean isCycle = true;
        int count;
        public ReturnType(boolean isCycle, int count) {
            this.isCycle = isCycle;
            this.count = count;
        }
    }
    public boolean canFinish(int numCourses, int[][] prerequisites) {   

        // sanity check

        // build graph
        Map<Integer, Course> graph = buildGraph(numCourses, prerequisites);
        // Set<Course> init = buildInit(graph);
        
        int globalCount = 0;
        for (int courseNumber: graph.keySet()) {
            Course init = graph.get(courseNumber);
            // if (init.prevCourse == null) {
            if (init.prevCourse.isEmpty()){
                ReturnType curResult  = dfs(init, graph);
                if (curResult.isCycle == true) {
                    return false;
                }
                globalCount += curResult.count;
            }
        }
        return globalCount == numCourses;
    }
    private ReturnType dfs(Course init, Map<Integer, Course> graph) {
        if (init.visiting == true) {
            return new ReturnType(true, 0);
        }
        if (init.visited == true) { // 注意这两个的顺序，如果你不是exclusive的状态
            return new ReturnType(false, 0);
        }

        init.visiting = true;
        int count = 1;
        for (Course next: init.nextCourse) {
            ReturnType nextResult = dfs(next, graph);
            if (nextResult.isCycle == true) {
                return new ReturnType(true, 0);
            }
            count += nextResult.count;
        }
        init.visited = true; // 注意，这里是先标visiting，然后再标visited，否则会出错。。。
        init.visiting = false; // 如果没有这一行，visited要在前面,
        return new ReturnType(false, count);
    }
    private Map<Integer, Course> buildGraph(int numCourses, int[][] prerequisites) {
        Map<Integer, Course> graph = new HashMap<>();
        for (int i = 0; i < numCourses; i++) {
            graph.put(i, new Course(i));
        }
        for (int[] depe: prerequisites) {
            int nextCourse = depe[0];
            int prevCourse = depe[1];
            Course next = graph.get(nextCourse);
            Course prev = graph.get(prevCourse);
            next.prevCourse.add(prev);
            prev.nextCourse.add(next);
        }
        return graph;
    } 
}
```

Method 3 dfs with enum

```java
class Solution {
    class Course {
        int courseNumber;
        Set<Course> prevCourse;
        Set<Course> nextCourse;
        State state;
        // = State.UNVISITED;
        public Course(int course) {
            this.courseNumber = course;
            this.prevCourse = new HashSet<>();
            this.nextCourse = new HashSet<>();
            this.state = State.UNVISITED;
        }
        @Override
        public int hashCode(){
            int hashCode = this.courseNumber  * 31 + 31;
            return hashCode;
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (obj == null) return false;
            if (this.getClass() != obj.getClass()) {
                return false;
            }
            Course that = (Course) obj;
            return this.courseNumber == that.courseNumber;
        }

    }
    class ReturnType{
        boolean isCycle = true;
        int count;
        public ReturnType(boolean isCycle, int count) {
            this.isCycle = isCycle;
            this.count = count;
        }
    }
    public boolean canFinish(int numCourses, int[][] prerequisites) {   

        // sanity check

        // build graph
        Map<Integer, Course> graph = buildGraph(numCourses, prerequisites);
        // Set<Course> init = buildInit(graph);
        
        int globalCount = 0;
        for (int courseNumber: graph.keySet()) {
            Course init = graph.get(courseNumber);
            if (init.prevCourse.isEmpty()){
                ReturnType curResult  = dfs(init, graph);
                // System.out.println(curResult.count);
                if (curResult.isCycle == true) {
                    return false;
                }
                globalCount += curResult.count;
            }
        }
        return globalCount == numCourses;
    }
    private ReturnType dfs(Course init, Map<Integer, Course> graph) {
        if (init.state == State.VISITED) {
            return new ReturnType(false, 0);
        }
        if (init.state == State.VISITING) { // 注意这两个的顺序，如果你不是exclusive的状态
            return new ReturnType(true, 0);
        }

        init.state = State.VISITING;
        int count = 1;
        for (Course next: init.nextCourse) {
            ReturnType nextResult = dfs(next, graph);
            // System.out.println(nextResult.count);
            // System.out.println(nextResult.isCycle);
            if (nextResult.isCycle == true) {
                return new ReturnType(true, 0);
            }
            count += nextResult.count;
        }
        init.state = State.VISITED; // 注意，这里是先标visiting，然后再标visited，否则会出错。。。
        // System.out.println(count);
        return new ReturnType(false, count);
    }
    private Map<Integer, Course> buildGraph(int numCourses, int[][] prerequisites) {
        Map<Integer, Course> graph = new HashMap<>();
        for (int i = 0; i < numCourses; i++) {
            graph.put(i, new Course(i));
        }
        for (int[] depe: prerequisites) {
            int nextCourse = depe[0];
            int prevCourse = depe[1];
            Course next = graph.get(nextCourse);
            Course prev = graph.get(prevCourse);
            next.prevCourse.add(prev);
            // System.out.println(next.prevCourse);
            prev.nextCourse.add(next);
            // System.out.println(prev.nextCourse);
        }
        return graph;
    } 
    private enum State {
        VISITED,
        VISITING,
        UNVISITED,
    }
}
```

Method 3 with bfs

```java
class Solution {
    class Course {
        int courseNumber;
        Set<Course> prevCourse;
        Set<Course> nextCourse;
        State state;
        int preCourseNumber;
        public Course(int course) {
            this.courseNumber = course;
            this.prevCourse = new HashSet<>();
            this.nextCourse = new HashSet<>();
            this.state = State.UNVISITED;
            this.preCourseNumber = 0;
        }
        @Override
        public int hashCode(){
            int hashCode = this.courseNumber  * 31 + 31;
            return hashCode;
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj) return true;
            if (obj == null) return false;
            if (this.getClass() != obj.getClass()) {
                return false;
            }
            Course that = (Course) obj;
            return this.courseNumber == that.courseNumber;
        }

    }
    class ReturnType{
        boolean isCycle = true;
        int count;
        public ReturnType(boolean isCycle, int count) {
            this.isCycle = isCycle;
            this.count = count;
        }
    }
    public boolean canFinish(int numCourses, int[][] prerequisites) {   

        // sanity check

        // build graph
        Map<Integer, Course> graph = buildGraph(numCourses, prerequisites);
        ReturnType result = bfs(graph);
        
        return result.count == numCourses;
    }
    private ReturnType bfs(Map<Integer, Course> graph) {
        Queue<Course> queue = new ArrayDeque<>();
        int count = 0;
        for (int courseNumber: graph.keySet()) {
            Course cur = graph.get(courseNumber);
            if (cur.prevCourse.isEmpty()) {
                count++;
                queue.offer(cur);
            }
        }
        boolean isCycle = false;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                Course cur = queue.poll();
                for (Course next: cur.nextCourse) {
                    next.preCourseNumber--;
                    if (next.preCourseNumber == 0) {
                        count++;
                        queue.offer(next);
                    }
                }
            }
        }
        return new ReturnType(isCycle, count);
    }
    private Map<Integer, Course> buildGraph(int numCourses, int[][] prerequisites) {
        Map<Integer, Course> graph = new HashMap<>();
        for (int i = 0; i < numCourses; i++) {
            graph.put(i, new Course(i));
        }
        for (int[] depe: prerequisites) {
            int nextCourse = depe[0];
            int prevCourse = depe[1];
            Course next = graph.get(nextCourse);
            next.preCourseNumber++;
            Course prev = graph.get(prevCourse);
            next.prevCourse.add(prev);
            prev.nextCourse.add(next);
        }
        return graph;
    } 
    private enum State {
        VISITED,
        VISITING,
        UNVISITED,
    }
}
```
