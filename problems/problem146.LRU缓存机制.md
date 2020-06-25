# 146. LRU缓存机制
LRU算法是啥  
就是一种缓存淘汰策略，如果缓存满了就要删除一些内容，给新内容腾位置。LRU全程是Least Recently Used，也就是说我们认为最近使用过的数据应该是有用的，  很久都没用过的数据应该是无用的，内存满了就优先删除很久没用过的数据。  
````cpp
/* 缓存容量为 2 */
LRUCache cache = new LRUCache(2);
// 你可以把 cache 理解成一个队列
// 假设左边是队头，右边是队尾
// 最近使用的排在队头，久未使用的排在队尾
// 圆括号表示键值对 (key, val)

cache.put(1, 1);
// cache = [(1, 1)]
cache.put(2, 2);
// cache = [(2, 2), (1, 1)]
cache.get(1);       // 返回 1
// cache = [(1, 1), (2, 2)]
// 解释：因为最近访问了键 1，所以提前至队头
// 返回键 1 对应的值 1
cache.put(3, 3);
// cache = [(3, 3), (1, 1)]
// 解释：缓存容量已满，需要删除内容空出位置
// 优先删除久未使用的数据，也就是队尾的数据
// 然后把新的数据插入队头
cache.get(2);       // 返回 -1 (未找到)
// cache = [(3, 3), (1, 1)]
// 解释：cache 中不存在键为 2 的数据
cache.put(1, 4);    
// cache = [(1, 4), (3, 3)]
// 解释：键 1 已存在，把原始值 1 覆盖为 4
// 不要忘了也要将键值对提前到队头
````
要实现时间复杂度为O(1)的put和get方法，那么就需要cache这个数据结构有以下条件：查找快，插入快，删除快，有顺序之分。  
哈希表查找快，但是数据无固定顺序；链表有顺序之分，插入删除快，但是查找慢。所以结合一下，形成一种新的数据结构：哈希链表。  
LRU缓存算法的核心数据结构就是哈希链表，双向链表和哈希表的结合体。
![image](https://github.com/xjcgerry/no-unemployment/blob/master/images/146-1.jpg)

````cpp
class LRUCache {
public:
    LRUCache(int capacity) {
        this->cap = capacity;
    }
    
    int get(int key) {
        auto it = map.find(key);
        if (it == map.end()) return -1;
        pair<int, int> kv = *map[key];
        cache.erase(map[key]);
        cache.push_front(kv);
        map[key] = cache.begin();
        return kv.second;
    }
    
    void put(int key, int value) {
        auto it = map.find(key);
        if (it == map.end()) {
            if (cache.size() == cap) {
                auto lastPair = cache.back();
                int lastKey = lastPair.first;
                map.erase(lastKey);
                cache.pop_back();
            }
            cache.push_front(make_pair(key, value));
            map[key] = cache.begin();
        } else {
            cache.erase(map[key]);
            cache.push_front(make_pair(key, value));
            map[key] = cache.begin();
        }
    }

private:
    int cap;
    list<pair<int, int>> cache;
    unordered_map<int, list<pair<int, int>>::iterator> map;
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
 ````
 * 问：为什么要在链表中同时存储key和val，而不是只存储val
 * 答：当缓存容量已满，我们不仅仅要删除最后一个Node节点，还要把map中映射到该节点的key同时删除，而这个key只能由Node得到。如果Node节点只存储val，那么我们无法得到key是什么，就无法删除map中的键，造成错误。
