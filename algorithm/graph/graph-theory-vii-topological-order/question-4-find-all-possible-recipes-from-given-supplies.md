# Question 4 Find All Possible Recipes from given Supplies

Step 1: modeling the question

* thisi is a graph problem

Step 2: build the Graph

* node/ vertex 具体的菜品名字
* edges：ingredients
* 要说出一句很有dependency的感觉的话要想做出recipsbread, 我得有 yeast 和flour
* prerequisites:要想上ai必须得先上bi

Step 3: Topological Sort

&#x20;first determine the dependency graph:

* recipes: bread, burger
* ingredients: \[flour, yeast], \[xxxx]
* ingredients-->对应的recipes

example:

* recipes = \["bread", "sandwich", "burger"]
* ingredients = \[\["yeast", "flour"], \["bread", "meat"], \["sandwich", "meat", "bread"]]
* supplies =\["yeast", "flour", "meat"]



Build Graph:



Details Logic：

* 这个题目要求return是所有能做出来的菜品的名字
* InDegree的选择：
  * Map\<String, Integer> inDegree
  * int\[] inDegree:将来你能知道yeast指向bread，bread的index是谁
* 题目问的是你所有能做出来的recipes的名字
  * 如果我每次exapnd一个菜。我就加到result里对么？
  * 有可能把supply或者半成品(ingredients)加到result了，我们得保证加入result里的知识recipes
  * 我们可以在release recipes的时候再加结果(generation)





```java
public List<String> findAllRecipes(String[] recipes, List<List<String>> ingredients, String[] supplies) {
    int[] inDegree = new int[recipes.length];
    //每个ingredients，被哪些recipes需要，记录需要它的recipes的index
    


}
private Map<String, List<Integer>> buildGraph(String[] recipes, List<List<String>> ingredients, String[] supplies) {
    Map<String, List<Integer>> graph = new HashMap<>();
    for (int recipesIndex = 0; recipesIndex < recipes.length; recipesIndex++) {
        for (String ingredient: ingredient[i]) {
            /*
            ingredient --> recipes
            first         second
            */
            graph.putIfAbsent(ingredient, new ArrayList<>());
            graph.get(ingredient).add(recipesIndex);
            inDegree[recipesIndex]++;
        }
    }

}
```

