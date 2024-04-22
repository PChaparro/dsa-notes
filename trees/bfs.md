# BFS 🔎

# When to use

- Find the shortest path from vertex `a` to all other vertices in an **unweighted** graph.

- Check if an element is present in a graph by traversing it level by level.

## Implementation

```cpp
// 🚨 Here we use a queue of `string` but  it could be a queue of any type that represents the nodes of the graph.
queue<string> pendingCombs;

// Start from some node
pendingCombs.push(INITIAL_COMB);
seen.insert(INITIAL_COMB);

while (!pendingCombs.empty())
{
  /**
    * 🚨  This needs to be assigned to a variable, using a for loop with
    * `pendingCombs.size()` as the condition WON'T work and will cause an
    * infinite loop.
  */
  int combsInCurrLvl = pendingCombs.size();

  while (combsInCurrLvl--)
  {
    string currComb = pendingCombs.front();
    pendingCombs.pop();

    if (currComb == target)
      return currLvl;

    // 🚨 This should be replaced by the logic to get the neighbor nodes of the current node
    for (int wheelToUpdate = 0; wheelToUpdate < currComb.size(); wheelToUpdate++)
    {
      string d = currComb, u = currComb;

      d[wheelToUpdate] = wrappedDown[currComb[wheelToUpdate]];
      if (seen.find(d) == seen.end())
      {
        /**
          * We push the "neighbor" and mark it as seen to prevent it to be pushed
          * again to the queue by another node in the current or next levels.
        */
        pendingCombs.push(d);
        seen.insert(d);
      }

      u[wheelToUpdate] = wrappedUp[currComb[wheelToUpdate]];
      if (seen.find(u) == seen.end())
      {
        /**
          * We push the "neighbor" and mark it as seen to prevent it to be pushed
          * again to the queue by another node in the current or next levels.
        */
        pendingCombs.push(u);
        seen.insert(u);
      }
    }
  }

  // After processing all the nodes in the current level, we move to the next level
  currLvl++;
}
```

## Resources

|                                            Link                                            | Type  | Language |
| :----------------------------------------------------------------------------------------: | :---: | :------: |
| [Algoritmos BFS y DFS (Recorridos en Grafos)](https://www.youtube.com/watch?v=_Yf8tneauJ8) | Video |    🇪🇸    |
