### Depth Limited Search

#### DFS but fixed depth traversal power

### C++
```cpp
#include <bits/stdc++.h>

using namespace std;

vector<vector<int>> graph;

bool depth_limited_search(int start, int goal, int depth_limit) {
    stack<pair<int, int>> s;
    vector<bool> visited(graph.size(), false);

    s.push({start, 0});

    while (!s.empty()) {
        int currentNode = s.top().first;
        int currentDepth = s.top().second;
        s.pop();

        if (currentNode == goal) {
            cout << "Goal found at depth " << currentDepth << endl;
            return true;
        }

        if (currentDepth < depth_limit) {
            visited[currentNode] = true;

            for (int neighbor : graph[currentNode]) {
                if (!visited[neighbor]) {
                    s.push({neighbor, currentDepth + 1});
                }
            }
        }
    }

    cout << "Goal not found within the depth limit." << endl;
    return false;
}

int main() {
    // Graph initialization
    graph.resize(7);

    graph[0] = {1, 3};
    graph[1] = {6};
    graph[2] = {1};
    graph[3] = {1, 6, 4};
    graph[4] = {2, 5};
    graph[5] = {2, 6};
    graph[6] = {4};

    int goal = 6;
    int start = 0;
    int depth_limit = 2;

    depth_limited_search(start, goal, depth_limit);

    return 0;
}

```