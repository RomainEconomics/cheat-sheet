# Dijkstra's Algorithm Explanation

Dijkstra's algorithm is used to find the shortest path between nodes in a graph.

## To have in mind

Djikstra's: not guaranteed to work when there are negative edges
Bellman-Ford: will not give the correct answer if there is a negative cycle but works with negative edges
Any negative cycle: the answer is always -infinity as you can just go through the negative cycle infinitely for an infinitely short distance

So before solving any shortest path problem, you can check all edges for negative values, and run a dfs for cycle detection and check if the cycle edges sum up to a negative value to figure out what case you're in

## Overview of the Algorithm

1. Initialize data structures for tracking distances, visited nodes, and predecessors
2. Start from the source node with a distance of 0
3. Explore the graph by always visiting the unvisited node with the smallest known distance
4. Update distances to neighbors if a shorter path is found
5. Reconstruct the path once the destination is reached

## Step-by-Step Explanation

### 1. Initialization

```python
def dijkstra(graph, src, dest):
    unvisited = set()
    predecessors = {}
    distances = {}
    for node in graph:
        unvisited.add(node)
        distances[node] = float("inf")
    distances[src] = 0
```

- We create three data structures:
  - `unvisited`: A set of all nodes we haven't processed yet
  - `predecessors`: A dictionary to track which node comes before each node in the shortest path
  - `distances`: A dictionary to store the shortest known distance from the source to each node
- All nodes start with an infinite distance except the source node, which starts at 0

### 2. Main Loop

```python
while len(unvisited):
    min_dist_node = get_min_dist_node(distances, unvisited)
    unvisited.remove(min_dist_node)

    if min_dist_node == dest:
        return get_path(dest, predecessors)
```

- In each iteration, we:
  - Find the unvisited node with the minimum distance (using `get_min_dist_node`)
  - Remove it from the unvisited set (mark it as visited)
  - If we've reached the destination, we reconstruct and return the path

### 3. Neighbor Processing

```python
for neighbor in graph[min_dist_node]:
    if neighbor not in unvisited:
        continue

    distance_so_far = distances[min_dist_node]
    distance_to_neighbor = graph[min_dist_node][neighbor]
    total_distance_to_neighbor = distance_so_far + distance_to_neighbor

    if total_distance_to_neighbor < distances.get(neighbor):
        distances[neighbor] = total_distance_to_neighbor
        predecessors[neighbor] = min_dist_node
```

- For each neighbor of the current node:
  - Skip if we've already visited this neighbor
  - Calculate the total distance to reach this neighbor through the current node
  - If this new path is shorter than any previously known path:
    - Update the distance to this neighbor
    - Set the current node as the predecessor for this neighbor

### 4. Helper Functions

```python
def get_min_dist_node(distances, unvisited):
    min_dist = float("inf")
    min_dist_node = None
    for v in unvisited:
        distance_so_far = distances[v]
        if distance_so_far < min_dist:
            min_dist = distance_so_far
            min_dist_node = v
    return min_dist_node
```

- This function finds the unvisited node with the smallest distance

```python
def get_path(dest, predecessors):
    path = []
    pred = dest
    while pred is not None:
        path.append(pred)
        pred = predecessors.get(pred, None)
    path.reverse()
    return path
```

- This function reconstructs the path from source to destination:
  - Start at the destination
  - Follow the predecessors backward to the source
  - Reverse the path to get the correct order (source to destination)

## Time and Space Complexity

- Time complexity: O(V² + E) where V is the number of vertices and E is the number of edges
  - The implementation could be improved to O((V + E) log V) using a priority queue
- Space complexity: O(V) for storing distances, predecessors, and the unvisited set

## Example Usage

This implementation uses an adjacency list representation of the graph, where each node has a dictionary of its neighbors and the distance to each neighbor.

```python
def dijkstra(
        graph: list[dict[str, dict[str, int]]],
        src: str,
        dest: str
):
    unvisited = set()
    predecessors = {}
    distances = {}
    for node in graph:
        unvisited.add(node)
        distances[node] = float("inf")
    distances[src] = 0

    while len(unvisited):
        min_dist_node = get_min_dist_node(distances, unvisited)
        unvisited.remove(min_dist_node)

        if min_dist_node == dest:
            return get_path(dest, predecessors)

        for neighbor in graph[min_dist_node]:
            if neighbor not in unvisited:
                continue

            distance_so_far = distances[min_dist_node]
            distance_to_neighbor = graph[min_dist_node][neighbor]
            total_distance_to_neighbor = distance_so_far + distance_to_neighbor

            if total_distance_to_neighbor < distances.get(neighbor):
                distances[neighbor] = total_distance_to_neighbor
                predecessors[neighbor] = min_dist_node


def get_path(dest, predecessors):
    path = []
    pred = dest
    while pred is not None:
        path.append(pred)
        pred = predecessors.get(pred, None)
    path.reverse()
    return path


def get_min_dist_node(distances, unvisited):
    min_dist = float("inf")
    min_dist_node = None
    for v in unvisited:
        distance_so_far = distances[v]
        if distance_so_far < min_dist:
            min_dist = distance_so_far
            min_dist_node = v
    return min_dist_node
```

Test:

```python
run_cases = [
    (
        {
            "Minas Tirith": {"Isengard": 4, "Gondor": 1},
            "Isengard": {"Minas Tirith": 4, "Bree": 3, "Mirkwood": 8},
            "Gondor": {"Minas Tirith": 1, "Bree": 2, "Misty Mountains": 6},
            "Bree": {"Gondor": 2, "Isengard": 3, "Mirkwood": 4},
            "Mirkwood": {"Bree": 4, "Isengard": 8, "Lothlorien": 2},
            "Misty Mountains": {"Gondor": 6, "Lothlorien": 8},
            "Lothlorien": {"Misty Mountains": 8, "Mirkwood": 2},
        },
        "Minas Tirith",
        "Lothlorien",
        ["Minas Tirith", "Gondor", "Bree", "Mirkwood", "Lothlorien"],
    ),
    (
        {
            "Minas Tirith": {"Isengard": 4, "Gondor": 1},
            "Isengard": {"Minas Tirith": 4, "Bree": 3, "Mirkwood": 8},
            "Gondor": {"Minas Tirith": 1, "Bree": 2, "Misty Mountains": 6},
            "Bree": {"Gondor": 2, "Isengard": 3, "Mirkwood": 4},
            "Mirkwood": {"Bree": 4, "Isengard": 8, "Lothlorien": 2},
            "Misty Mountains": {"Gondor": 6, "Lothlorien": 8},
            "Lothlorien": {"Misty Mountains": 8, "Mirkwood": 2},
        },
        "Isengard",
        "Gondor",
        ["Isengard", "Bree", "Gondor"],
    ),
]

submit_cases = run_cases + [
    (
        {"Minas Tirith": {"Isengard": 2}, "Isengard": {"Minas Tirith": 2}},
        "Minas Tirith",
        "Isengard",
        ["Minas Tirith", "Isengard"],
    ),
    (
        {
            "Erebor": {"Minas Tirith": 2, "Isengard": 1},
            "Minas Tirith": {"Erebor": 3, "Isengard": 4, "Gondor": 8},
            "Isengard": {"Erebor": 4, "Minas Tirith": 2, "Bree": 2},
            "Gondor": {"Minas Tirith": 2, "Bree": 7, "Osgiliath": 4},
            "Bree": {"Isengard": 1, "Gondor": 11, "Osgiliath": 5},
            "Osgiliath": {"Gondor": 3, "Bree": 5},
        },
        "Erebor",
        "Osgiliath",
        ["Erebor", "Isengard", "Bree", "Osgiliath"],
    ),
    (
        {
            "Erebor": {"Minas Tirith": 2, "Isengard": 1},
            "Minas Tirith": {"Erebor": 3, "Isengard": 4, "Gondor": 8},
            "Isengard": {"Erebor": 4, "Minas Tirith": 2, "Bree": 2},
            "Gondor": {"Minas Tirith": 2, "Bree": 7, "Osgiliath": 4},
            "Bree": {"Isengard": 1, "Gondor": 11, "Osgiliath": 5},
            "Osgiliath": {"Gondor": 3, "Bree": 5},
        },
        "Minas Tirith",
        "Bree",
        ["Minas Tirith", "Isengard", "Bree"],
    ),
]


def test(graph, src, dest, expected_output):
    try:
        print("---------------------------------")
        print(f"Graph:")
        for k, v in graph.items():
            print(f" Vertex {k}: {v}")
        print(f"\n - Src: {src}")
        print(f" - Dest: {dest}\n")
        print(f"Expected Path: {expected_output}")
        result = dijkstra(graph, src, dest)
        print(f"Actual Path: {result}\n")
        if result == expected_output:
            print("Pass")
            return True
        print("Fail")
        return False
    except Exception as e:
        print("Fail")
        print(e)
        return False


def main():
    passed = 0
    failed = 0
    skipped = len(submit_cases) - len(test_cases)
    for test_case in test_cases:
        correct = test(*test_case)
        if correct:
            passed += 1
        else:
            failed += 1
    if failed == 0:
        print("============= PASS ==============")
    else:
        print("============= FAIL ==============")
    if skipped > 0:
        print(f"{passed} passed, {failed} failed, {skipped} skipped")
    else:
        print(f"{passed} passed, {failed} failed")


test_cases = submit_cases
if "__RUN__" in globals():
    test_cases = run_cases

main()
```
