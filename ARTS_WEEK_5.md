# 第五周ARTS

# Algorithm
## 1.strStr()
Implement strStr().
```
Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.
Example 1:
Input: haystack = "hello", needle = "ll"
Output: 2
Example 2:
Input: haystack = "aaaaa", needle = "bba"
Output: -1
Clarification:
What should we return when needle is an empty string? This is a great question to ask during an interview.
For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().
```

```c++
//库函数解法：
class Solution {
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(needle.empty())
            return 0;
        int pos=haystack.find(needle);
        return pos;
    }
};
//BF算法 暴力破解:时间复杂度O(M*N)O(M∗N)
```

```c++
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(needle.empty())
            return 0;
        
        int i=0,j=0;
        while(haystack[i]!='\0'&&needle[j]!='\0')
        {
            if(haystack[i]==needle[j])
            {
                i++;
                j++;
            }
            else
            {
                i=i-j+1;
                j=0;
            }
        }
        if(needle[j]=='\0')
            return i-j;
        
        return -1;
    }
};
//还有典型的KMP解法，由于知识点还没覆盖到；等待有时间而刷的时候后头过来看。
```
# Tips
[matlab2c使用c++实现matlab函数系列教程-conv函数](https://blog.csdn.net/luanpeng825485697/article/details/77686595?tdsourcetag=s_pcqq_aiomsg)     
下午在实验室偶然听到同学被一个问题困惑到，如何在c++中实现两个未知向量的卷积和并输出结果？显而易见，造轮子的技术我们还不能掌握、另外在这么发达的开源时代 我们所拥有的现成的库函数一骡子。
助人为乐是一种美德，给你个反馈会让人感到快乐，毫无疑问，he got it!快乐当中自己也收获了成长。     
原来要下载matlab2c中的动态链接库 matlab2c.lib中即有conv现成的卷积函数调用。
动态链接库（DLL）是英文 Dynamic Link Library 的缩写，它是一种不可执行的二进制程序文件，但可以被其他程序调用。
# Review
[Code Review Best Practices](https://medium.com/palantir/code-review-best-practices-19e02780015f)

# Share
《小狗钱钱》国外儿童商财指定读本，可悲的我到了第二个本命年才接触到，受益颇多。    
种一棵树的最好时机是十年前，还有现在。！
