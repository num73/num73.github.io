**原文链接**：[MEX (minimal excluded) of a sequence - Algorithms for Competitive Programming (cp-algorithms.com)](https://cp-algorithms.com/sequences/mex.html)

# MEX(minimal excluded) of a sequence

## 问题

给一个大小为$N$的数组$A$。从中找到最小的没有出现过的非负整数，这个数一般被叫做**MEX(minimal excluded)**。
$$
mex(\{0,1,3,4,5\}) = 3\\
mex(\{0,1,2,3,4\}) = 5 \\
mex(\{1,2,3,4,5\}) = 0
$$
注意到，大小为$N$的数组的MEX不可能比$N$大。

最简单的求MEX的方法是把$A$的所有元素都放到一个set里，这样就可以很快地检查一个数是否在这个集合里。只要我们按顺序检查从$0$到$N$的所有数是否在集合里，如果当前数字不在集合里，就返回这个数。

## 代码实现

```c++
int mex(vector<int> const& A) {
    set<int> b(A.begin(), A.end());

    int result = 0;
    while (b.count(result))
        ++result;
    return result;
}
```

如果需要在$O(N)$的时间内计算MEX，可以使用一个bool类型的vector来代替集合，这样我们需要的就是和$A$一样大的一个数组。

```c++
int mex(vector<int> const& A) {
    static bool used[MAX_N+1] = { 0 };

    // mark the given numbers
    for (int x : A) {
        if (x <= MAX_N)
            used[x] = true;
    }

    // find the mex
    int result = 0;
    while (used[result])
        ++result;

    // clear the array again
    for (int x : A) {
        if (x <= MAX_N)
            used[x] = false;
    }

    return result;
}
```

这种方法很快，但是也仅仅是在当我们只需要计算一次MEX时才好用。如果你要一次又一次地计算MEX，这样就慢了。所以我们需要更好的方法。

## 带更新的MEX

问题：改变数组里的单个数，在每次更新后都计算数组里新的MEX。

需要使用更好的数据结构才能有效地解决这个问题。

一种方法是计算从$0$到$N$的数出现的频率，然后用一个树形的数据结构比如线段树或treap来维护这些频率。每一个节点来维护一个区间里数的频率，并且存储当前区间中出现的不同的数的数量。每次更新需要$O(logN)$的时间，通过二分在树上查找MEX需要$O(logN)$的时间。

另一种方法是使用STL中的`map`和`set`来计算。用一个`map`来存储每个数出现的频率，用一个`set`来代表当前数组中没有出现的数。因为`set`是有序的，`*set.begin()`就是我们要求的MEX。需要用$O(NlogN)$的时间进行预处理，每次MEX计算的时间为$O(1)$，更新需要的时间为$O(logN)$。

```c++
class Mex {
private:
    map<int, int> frequency;
    set<int> missing_numbers;
    vector<int> A;

public:
    Mex(vector<int> const& A) : A(A) {
        for (int i = 0; i <= A.size(); i++)
            missing_numbers.insert(i);

        for (int x : A) {
            ++frequency[x];
            missing_numbers.erase(x);
        }
    }

    int mex() {
        return *missing_numbers.begin();
    }

    void update(int idx, int new_value) {
        if (--frequency[A[idx]] == 0)
            missing_numbers.insert(A[idx]);
        A[idx] = new_value;
        ++frequency[new_value];
        missing_numbers.erase(new_value);
    }
};
```

