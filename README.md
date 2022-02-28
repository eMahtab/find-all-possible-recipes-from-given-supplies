# Find all possible recipes from given supplies
## https://leetcode.com/problems/find-all-possible-recipes-from-given-supplies


## Implementation 1 : Topological Sort
```java
class Solution {
    public List<String> findAllRecipes(String[] recipes, List<List<String>> ingredients, 
    String[] supplies) {
        List<String> result = new ArrayList<>();
        Queue<String> q = new ArrayDeque<>();
        for(String supply : supplies) {
            q.add(supply);
        }
        Map<String,Set<String>> map = new HashMap<>();
        for(int i = 0; i < recipes.length; i++) {
            map.putIfAbsent(recipes[i], new HashSet<String>());
            for(String ingredient : ingredients.get(i)) {
                map.get(recipes[i]).add(ingredient);
            }
        }
        while(!q.isEmpty()) {
            String ingredient = q.remove();
            for(String recipe : map.keySet()) {
                if(map.get(recipe).contains(ingredient)) {
                    map.get(recipe).remove(ingredient);
                    if(map.get(recipe).size() == 0) {
                        result.add(recipe);
                        q.add(recipe);
                    }
                }
            }
        }
        return result;
    }
}
```
