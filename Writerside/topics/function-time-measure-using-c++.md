# 使用c/c++测试函数运行时间

```c++
#include <iostream>
#include <chrono>
#include <string.h>
#include <time.h>
#include <typeinfo>
using namespace std;

char c[200];
char *p = (char*)malloc(sizeof(char));
void init() {
    memset(c, 'a', sizeof(c));
}
void fun() {
    *p = c[0];
}

int main() {
    init();
    auto before = chrono::system_clock::now();
    fun();
    auto after = chrono::system_clock::now();

    auto duration = chrono::duration_cast<chrono::nanoseconds>(after - before);
    cout << duration.count() << endl;

    struct timespec t1, t2;
    clock_gettime(CLOCK_MONOTONIC, &t1);
    fun();
    clock_gettime(CLOCK_MONOTONIC, &t2);
    cout << t2.tv_sec - t1.tv_sec + t2.tv_nsec - t2.tv_nsec << endl;
    return 0;
}

```