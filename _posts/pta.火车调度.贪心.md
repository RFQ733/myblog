# 列车调度

两端分别是一条入口（Entrance）轨道和一条出口（Exit）轨道，它们之间有`N`条平行的轨道。每趟列车从入口可以选择任意一条轨道进入，最后从出口离开。在图中有9趟列车，在入口处按照{8，4，2，5，3，9，1，6，7}的顺序排队等待进入。如果要求它们必须按序号递减的顺序从出口离开，则至少需要多少条平行铁轨用于调度？

## Tag：

<strong>贪心</strong> <strong>set</strong> <strong>PTA</strong> <strong>set.upper_bound()</strong> <strong>algorithm的upper_bound()</strong>

## Thinking

首先，你应该想到这是一个贪心的题（反正我想不到，头秃）。

知道贪心以后就很简单了，我一开始想使用vector  在每次循环中使用sort，并使用使用自己实现的find_upper_bound 方法进行插入修改val；显然time-out了。

然后我使用了set进行进一步的优化，结果因为调用的upper_bound函数是algorithm库中又time-out了。

```cpp
low=lower_bound (v.begin(), v.end(), 11); 
up= upper_bound (v.begin(), v.end(), 11);
```

最终，使用了set . upper_bound(num)实现了解题。



## Code

~~~ cpp
#include<bits/stdc++.h>
using namespace std;
int main()
{
    int n;
    scanf("%d",&n);
    set<int>ans;
    int s;
    scanf("%d",&s);
    ans.insert(s);
    n--;
    while(n--){
        scanf("%d",&s);
        set<int>::iterator m = ans.begin();
        m  = ans.end();
        m--;
        if(*m<s){
            ans.insert(s);
            continue;
        }
        m = ans.upper_bound(s);
        ans.erase(m);
        ans.insert(s);
    }
    printf("%d",ans.size());
    return 0;
}
~~~









