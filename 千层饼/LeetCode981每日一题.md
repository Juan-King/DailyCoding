### LeetCode981每日一题

#### 基于时间的键值存储

```java
class TimeMap {
    /** Initialize your data structure here. */
    HashMap<String, TreeMap<Integer,String>> map;
    Comparator<Integer> comparator = new Comparator<Integer>() {
        @Override
        public int compare(Integer o1, Integer o2) {
            return o2-o1;//倒序
        }
    };
    public TimeMap() {
        map = new HashMap<>();
    }
    public void set(String key, String value, int timestamp) {
        if(map.containsKey(key)){//已有相同key存储
            map.get(key).put(timestamp,value);//更新
        }else {
            TreeMap<Integer,String> m_v = new TreeMap<>(comparator);
            m_v.put(timestamp,value);
            map.put(key,m_v);
        }
    }
    public String get(String key, int timestamp) {
        if(map.containsKey(key)){
            TreeMap<Integer,String> res = map.get(key);
            for(Map.Entry<Integer,String> entry: res.entrySet()){
                if(entry.getKey()<=timestamp){
                    return entry.getValue();
                }
            }
        }
        return "";
    }
}
```

