# Dijkstra's Algorithm 🚀

## When to use

Find the shortest path from vertex `a` to all other vertices in a **non-negative** weighted graph.

## Implementation

```cpp
class Solution
{
private:
  // adj[A] = List of pairs (B, C) where B is the vertex and C is the cost to go from A to B
  unordered_map<int, vector<pair<int, long long int>>> adj;

public:
  /**
    * @param from The vertex where the edge starts
    * @param distances Pointer to the array to store the distances from the vertex `from` to all other vertices
    */
  void dijkstra(int from, lli *distances)
  {
    // We use a priority queue so we always get the vertex with the smallest distance
    priority_queue<pair<int, long long int>, vector<pair<int, long long int>>, greater<>> pendingVertex;

    // Start from the vertex `from` with a cost of 0 (Go to itself costs 0)
    pendingVertex.push({from, 0});

    // Update the distance to itself in the distances array
    distances[from] = 0;

    while (!pendingVertex.empty())
    {
      pair<int, long long int> currentPair = pendingVertex.top();
      pendingVertex.pop();

      int currentVertex = currentPair.first;
      int accCostToCurrentVertex = currentPair.second;

      if (accCostToCurrentVertex > distances[currentVertex])
        continue;

      for (pair<int, long long int> adjacent : this->adj[currentVertex])
      {
        int neighborVertex = adjacent.first;
        lli goToNeighborCost = adjacent.second;

        // The neighbor wasn't visited or we found a better path to it
        if (accCostToCurrentVertex + goToNeighborCost < distances[neighborVertex])
        {
          // Update the distance to the neighbor to the new minimum cost
          distances[neighborVertex] = accCostToCurrentVertex + goToNeighborCost;

          // Add the neighbor to be analyzed in next iterations
          pendingVertex.push({neighborVertex, distances[neighborVertex]});
        }
      }
    }
  };
}
```

## Resources

|                                                       Link                                                        | Type  | Language |
| :---------------------------------------------------------------------------------------------------------------: | :---: | :------: |
| [Dijkstra's Algorithm - Single Source Shortest Path - Greedy Method](https://www.youtube.com/watch?v=XB4MIexjvY0) | Video |    🇺🇸    |
|      [Implementing Dijkstra's Algorithm with a Priority Queue](https://www.youtube.com/watch?v=CerlT7tTZfY)       | Video |    🇺🇸    |
