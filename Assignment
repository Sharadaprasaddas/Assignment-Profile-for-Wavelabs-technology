#include <iostream>
#include <vector>
#include <algorithm>

class UnionFind {
private:
    std::vector<int> parent;
    std::vector<int> size;
    int count;
public:
    UnionFind(int n) {
        parent.resize(n);
        size.resize(n, 1);
        count = n;
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }

    int find(int p) {
        while (p != parent[p]) {
            parent[p] = parent[parent[p]];
            p = parent[p];
        }
        return p;
    }

    void unite(int p, int q) {
        int root_p = find(p);
        int root_q = find(q);
        if (root_p == root_q) {
            return;
        }
        if (size[root_p] < size[root_q]) {
            std::swap(root_p, root_q);
        }
        parent[root_q] = root_p;
        size[root_p] += size[root_q];
        count--;
    }

    int getCount() {
        return count;
    }
};

int makeConnected(int n, std::vector<std::vector<int>>& connections) {
    if (connections.size() < n - 1) {
        return -1;
    }

    UnionFind uf(n);
    std::vector<std::pair<int, int>> available;
    for (auto& c : connections) {
        int a = c[0];
        int b = c[1];
        if (uf.find(a) == uf.find(b)) {
            available.push_back({a, b});
        } else {
            uf.unite(a, b);
        }
    }

    while (uf.getCount() > 1 && !available.empty()) {
        auto [a, b] = available.back();
        available.pop_back();
        uf.unite(a, b);
    }

    if (uf.getCount() == 1) {
        return connections.size() - (n - 1);
    } else {
        return -1;
    }
}

int main() {
    int n = 4;
    std::vector<std::vector<int>> connections{{0, 1}, {0, 2}, {1, 2}};
    int result = makeConnected(n, connections);
    std::cout << result << std::endl; // Output: 1
    return 0;
}
