# LEETCODE-Array-874
Let's do a dry run of the `robotSim` function with an example to understand how it works. 

### Example Input:
- `commands = [4, -1, 3, -2, 2]`
- `obstacles = [[2, 4], [3, 5]]`

### Initial Setup:
- `dirs = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}}`: This represents the four possible directions (north, east, south, west).
- `ans = 0`: This will store the maximum Euclidean distance squared that the robot reaches from the origin.
- `d = 0`: Initially facing north.
- `x = 0, y = 0`: The robot starts at the origin.
- `obstaclesSet`: A set of obstacle positions for quick lookup.

### Step-by-Step Execution:

1. **Process the obstacles**:
   - The obstacles `[[2, 4], [3, 5]]` are stored in the `obstaclesSet` as pairs.

2. **First Command: `4` (move 4 steps forward)**:
   - The robot is facing north (direction `d = 0`).
   - Attempt to move forward 4 steps:
     - Step 1: `(x, y) = (0, 1)`
     - Step 2: `(x, y) = (0, 2)`
     - Step 3: `(x, y) = (0, 3)`
     - Step 4: `(x, y) = (0, 4)`
   - Update `ans = max(ans, x*x + y*y) = max(0, 0*0 + 4*4) = 16`.

3. **Second Command: `-1` (turn right)**:
   - Turn right: `d = (d + 1) % 4 = 1` (now facing east).

4. **Third Command: `3` (move 3 steps forward)**:
   - The robot is facing east (direction `d = 1`).
   - Attempt to move forward 3 steps:
     - Step 1: `(x, y) = (1, 4)`
     - Step 2: `(x, y) = (2, 4)` (but this is an obstacle, so stop moving).
   - The robot doesn't move past `(2, 4)` due to the obstacle.
   - The maximum distance remains `ans = 16`.

5. **Fourth Command: `-2` (turn left)**:
   - Turn left: `d = (d + 3) % 4 = 0` (now facing north again).

6. **Fifth Command: `2` (move 2 steps forward)**:
   - The robot is facing north (direction `d = 0`).
   - Attempt to move forward 2 steps:
     - Step 1: `(x, y) = (2, 5)`
   - There is no obstacle in this direction.
   - Update `ans = max(ans, x*x + y*y) = max(16, 2*2 + 5*5) = 29`.

### Result:
- The final maximum Euclidean distance squared is `29`.

### Code Issues:
There's a mistake in the code: the movement step calculation incorrectly references the directions using `dirs[d]` and `dirs[d+1]`. It should be:
```java
if (obstaclesSet.contains(new Pair<>(x + dirs[d][0], y + dirs[d][1]))) {
  break;
}
x += dirs[d][0];
y += dirs[d][1];
```
This ensures that the correct direction is used for both `x` and `y` coordinates.
