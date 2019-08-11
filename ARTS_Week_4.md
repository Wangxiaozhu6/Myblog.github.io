# Algorithm
## 1.Unique Character in a String

*Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.
```
Examples:
s = "leetcode"
return 0.
s = "loveleetcode",
return 2.
Note: You may assume the string contain only lowercase letters.
```
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        vector<int> v;
        v.resize(26,0);
        for(int i = 0; i< s.length(); ++i)           //0-25代表字母 见到一个字母就+1
        {
            v[s[i]-'a']++;
        }
        
        for(int i =0; i <s.length();++i)            //遍历原字符串，找到词频只有一次的就直接返回i
        {
            if(v[s[i]-'a'] == 1)
            {
                return i;
            }
        }
        return -1;
    }
};
//将数量为26空间大小整形容器用来放置每一个来输入的字符，一次遍历放置字符并用count函数进行计数；再用一次遍历来统计词频只有一次的字符即是First Unique Character in a String。
```

*根据提示使用哈希映射
遍历一遍字符串记录每个字母出现的次数
遍历hashmap，找出第一个出现次数只有一次的字符
```c++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char,int> hashmap;
        for(auto i : s){
            if(hashmap.count(i))    hashmap[i] += 1;
            else    hashmap[i] = 1;
        }
        for(int j = 0; s[j] != '\0'; ++ j)  if(hashmap[s[j]] == 1)  return j;
        return -1;
    }
};
```
## 2.反转字符串

*Write a function that reverses a string. The input string is given as an array of characters char[].
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
You may assume all the characters consist of printable ascii characters.
```
Example 1:
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
Example 2:
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

自己提交的代码：
```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        int n=s.size();
        for(int i=0;i<(n/2);i++)
        {
            swap(s[i],s[n-i-1]);
        }
        return;
        
    }
};
//运用STL库中swap交换函数进行逐个字符的翻转。
```
# Review

# Share

# Tip
**今天在Leetcode刷提时显现的错误解决方案。 

error:control reaches end of non-void function[-Werror=return-type]
问题场景描述：leetcode刷题时遇到这类报错，代码没问题，可就是编译不通过，很是怀疑人生。
问题解决：在函数的最后添加一条return语句，只要返回的数据类型对即可！记住，一定要返回，虽然永远也用不上。
