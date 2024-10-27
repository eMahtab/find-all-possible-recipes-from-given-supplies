# Find all possible recipes from given supplies
## https://leetcode.com/problems/find-all-possible-recipes-from-given-supplies


## Implementation 1 : Topological Sort
```java
class Solution {
    public List<String> findAllRecipes(String[] recipes, List<List<String>> ingredients, String[] supplies) {
        Map<String,Set<String>> map = new HashMap<>();
        for(int i = 0; i < recipes.length; i++) {
            String recipe = recipes[i];
            map.putIfAbsent(recipe, new HashSet<String>());
            List<String> items = ingredients.get(i);
            for(String item : items) {
                map.get(recipe).add(item);
            }
        }
        List<String> result = new ArrayList<String>();
        Queue<String> queue = new LinkedList<>();
        for(String supply : supplies)
           queue.add(supply);
        while(!queue.isEmpty()) {
            String supply = queue.remove();
            for(String recipe : map.keySet()) {
                Set<String> items = map.get(recipe);
                if(items.contains(supply)) {
                    items.remove(supply);
                    if(items.size() == 0) {
                        result.add(recipe);
                        queue.add(recipe);
                    }
                }
            }
        }
        return result;
    }
}
```
