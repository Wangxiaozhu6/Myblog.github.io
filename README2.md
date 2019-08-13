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

根据提示使用哈希映射
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

## 3.有效的字母异位词

*Given two strings s and t , write a function to determine if t is an anagram of s.
```
Example 1:
Input: s = "anagram", t = "nagaram"
Output: true
Example 2:
Input: s = "rat", t = "car"
Output: false
Note:
You may assume the string contains only lowercase alphabets.
Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?
```

提交代码：
```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        vector<int>s1(26,0);
        vector<int>t1(26,0);
        if(s.size()==t.length())
        {
            for(int i=0;i<s.size();i++)
            {
                s1[s[i]-'a']++;
                t1[t[i]-'a']++;
             }
            if(s1==t1)
                return true;
        }

        return false;
        
    }
};
//还是比较简单的（看过详解之后），利用桶的方法解决问题。开辟两个相同空间的整型容器，分别按照26个字母进行分别储存；并记录和叠加其字符出现的次数，若是两个异位的字符串则两容器相等作为判断依据。
```

## 4.验证回文字符串

*Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.
Note: For the purpose of this problem, we define empty string as valid palindrome.
```
Example 1:
Input: "A man, a plan, a canal: Panama"
Output: true
Example 2:
Input: "race a car"
Output: false
```

提交代码
```c++
class Solution {
public:
    bool isPalindrome(string s) {
        transform(s.begin(), s.end(), s.begin(), ::tolower);
        
        stack<int> intstack;
        
        for(int i=0;i<s.length();i++)
        {
            if(s[i]!=' '&&s[i]!=','&&s[i]!=':')
                {
                intstack.push(s[i]);
                 }
        }
        stack<int> s2;
        int k=intstack.size();
        
        for(int j=0;j<k;j++)
        {
            s2.push(intstack.top());
            intstack.pop();
        }

        if(intstack==s2)
            return true;
        else{
            return false;}
    }
};
//先将整个字符串中字母变为小写tolower();通过栈的先进后出的特性进行字符反转；最终比较两个栈是否相等作为判别依据。（这里可能存在问题。无法编译成功！）


class Solution {
public:
	bool isPalindrome(string s) {
		string s1;
		for (int i = 0; i < s.length(); i++)
		{
			if (s[i] == ' ')
			{
				i = s.find_first_not_of(' ',i);//从第i位置开始找第一个不为空格的位置
                if(i==-1) 
                    break;
			}
			if ((s[i] >= 'A'&&s[i] <= 'Z') || (s[i] >= 'a'&&s[i] <= 'z') || (s[i] >= '0'&&s[i] <= '9'))//是数字或者字母
			{
				if (s[i] >= 'A'&&s[i] <= 'Z')//大写转小写
				{
					s[i] = (s[i] + 32);
					s1 = s1 + s[i];
				}
				else
				{
					s1 = s1 + s[i];
				}
			}
			else continue;
		}
		string ress1 = s1;
		std::reverse(ress1.begin(), ress1.end());//回转字符串
		if (ress1 == s1)//若相等
			return true;
		else return false;
	}
};
//跟自己采用的思想类似，不同的是考虑的更加全面，且直接用reverse()进行反转省事很多；但在测试样例出现过长的字符串也会出现问题，比如内存分配过大，超出限制等。

双指针法：
class Solution {
public:
    bool isPalindrome(string s) {
        // 双指针
        if(s.size() <= 1) return true;
        int i = 0, j = s.size() - 1;
        while(i < j){
            while(i < j && !isalnum(s[i])) // 排除所有非字母或数字的字符
                i++;
            while(i < j && !isalnum(s[j]))
                j--;
            if(tolower(s[i++]) != tolower(s[j--])) //统一转换成小写字母再比较
                return false;
        }
        return true;
    }
};
//实为巧妙，通过头指针尾指针分别将字母或数字和其它进行计数；巧妙地运用了isalnum(char c):判断字符变量c是否为字母或数字，若是则返回非零，否则返回零；（分别将首尾字符进行比较，不相等即返回false ）    
tolower(char c):把字母字符转换成小写,非字母字符不做出处理。
```
# Review
[Can We Really Trust Digital Banks?](https://onezero.medium.com/how-much-can-we-really-trust-digital-banks-7f4a4416a48e)    
这篇文章，没啥营养。更像是一片自媒体的无厘头论述，还不如六级或考研一篇阅读来的好。针对快速发展的数字银行，在享受其带来的快捷、方便的同时，用户的PIN码被泄露了从来引发的举例讨论。从丑闻比较少的MONZO到22，最终针对数字银行再次扩张而表示了个人的担忧，但所有的问题到现在都是unanswerable，看的我也是云里雾里，头皮发麻。
# Share

# Tip
**今天在Leetcode刷提时显现的错误解决方案。 

error:control reaches end of non-void function[-Werror=return-type]
问题场景描述：leetcode刷题时遇到这类报错，代码没问题，可就是编译不通过，很是怀疑人生。
问题解决：在函数的最后添加一条return语句，只要返回的数据类型对即可！记住，一定要返回，虽然永远也用不上。
