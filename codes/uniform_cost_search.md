### Uniform Cost Search : 
##### Given a directed graph with associate cost of moving from one node to another, find the path with the smallest cost: 
### C++
###
```cpp
#include <bits/stdc++.h>

using namespace std;

// Graph representation
vector<vector<int>> graph;
map<pair<int, int>, int> cost;

int uniform_cost_search(int start, int goal) {
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    map<int, int> distance;

    pq.push({0, start});
    distance[start] = 0;

    while (!pq.empty()) {
        int currentCost = pq.top().first;
        int currentNode = pq.top().second;
        pq.pop();

        if (currentNode == goal) {
            return currentCost;
        }

        for (int neighbor : graph[currentNode]) {
            int newCost = currentCost + cost[{currentNode, neighbor}];

            if (distance.find(neighbor) == distance.end() || newCost < distance[neighbor]) {
                distance[neighbor] = newCost;
                pq.push({newCost, neighbor});
            }
        }
    }

    return INT_MAX;
}

int main() {

    graph.resize(7);

    // Directed graph
    graph[0] = {1, 3};
    graph[1] = {6};
    graph[2] = {1};
    graph[3] = {1, 6, 4};
    graph[4] = {2, 5};
    graph[5] = {2, 6};
    graph[6] = {4};

    // Costs
    cost[{0, 1}] = 2;
    cost[{0, 3}] = 5;
    cost[{1, 6}] = 1;
    cost[{3, 1}] = 5;
    cost[{3, 6}] = 6;
    cost[{3, 4}] = 2;
    cost[{2, 1}] = 4;
    cost[{4, 2}] = 4;
    cost[{4, 5}] = 3;
    cost[{5, 2}] = 6;
    cost[{5, 6}] = 3;
    cost[{6, 4}] = 7;

    // Goal state
    int goal = 6;
    
    // Start state
    int start = 0;

    int minCost = uniform_cost_search(start, goal);

    if (minCost != INT_MAX) {
        cout << "Minimum cost from " << start << " to " << goal << " is = " << minCost << endl;
    } else {
        cout << "Goal is not reachable from the start." << endl;
    }

    return 0;
}

```