``` java
import static java.util.stream.IntStream.range;

interface Remover {
  static int[] removeSmallest(int[] numbers) {
    int min = range(0, numbers.length).reduce((i, j) -> numbers[i] > numbers[j] ? j : i).orElse(-1);
    return range(0, numbers.length).filter(i -> i != min).map(i -> numbers[i]).toArray();
  }
}
```


### Example Execution

For the input `numbers = {5, 3, 2, 1, 4}`:

- **Finding the Smallest Index**:
    
    - `range(0, 5)` generates the stream `[0, 1, 2, 3, 4]`.
    - `reduce((i, j) -> numbers[i] > numbers[j] ? j : i)`:
        - Compares indices:  
            `0 (5)` vs `1 (3)` → keeps `1 (3)`.  
            `1 (3)` vs `2 (2)` → keeps `2 (2)`.  
            `2 (2)` vs `3 (1)` → keeps `3 (1)`.  
            `3 (1)` vs `4 (4)` → keeps `3 (1)`.
        - Result: `min = 3 (1)`.
- **Building the New Array**:
    
    - `range(0, 5)` again generates `[0, 1, 2, 3, 4]`.
    - `filter(i -> i != 3)` excludes `3`.
    - `map(i -> numbers[i])` maps indices `[0, 1, 2, 4]` to values `[5, 3, 2, 4]`.
    - `toArray()` converts this to the array `{5, 3, 2, 4}`.