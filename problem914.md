# 914. 卡牌分组
## 暴力法
计算容器中每个数出现的次数，对X从2开始遍历，首先判断能不能被整除size，如果可以在判断能不能整除每个数出现的次数。
````cpp
class Solution {
    int count[1000];
public:
    bool hasGroupsSizeX(vector<int>& deck) {
        int size = deck.size();
        if (size == 1) return false;
        for (int c:deck) count[c]++;

        vector<int> values;
        for (int i = 0; i < 1000; i++) {
            if (count[i] > 0)
                values.push_back(count[i]);
        }

        for (int i = 2; i <= size; i++) {
            if (size % i == 0) {
                bool flag = 1;
                for (int v:values) {
                    if (v % i != 0) {
                        flag = 0;
                        break;
                    }
                }
                if (flag) return true;
            }
        }
        return false;
    }
};
````
## 最大公约数
````cpp
class Solution {
    int count[1000];
public:
    bool hasGroupsSizeX(vector<int>& deck) {
        int size = deck.size();
        if (size == 1) return false;
        for (int c:deck) count[c]++;    //统计每个数字出现的次数

        int g = -1;
        for (int i = 0; i < 1000; i++) {
            if (count[i] > 0) {
                if (g == -1)
                    g = count[i];
                else
                    g = gcd(g, count[i]);
            }
        }
        return g >= 2;
    }

    //最大公约数 递归法
    int gcd(int x, int y) {
            return x == 0 ? y : gcd(y %x, x);
    }
};
````
