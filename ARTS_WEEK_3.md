# Algorithm
## 1.旋转数组
* 给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。
示例 1:    
```
输入: [1,2,3,4,5,6,7] 和 k = 3    
输出: [5,6,7,1,2,3,4]    
```
示例 2:
```
输入: [-1,-100,3,99] 和 k = 2         
输出: [3,99,-1,-100]        
```     
说明:         
尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
要求使用空间复杂度为 O(1) 的 原地 算法。

提交代码：
```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if(k>nums.size())
            k=k%nums.size();
        //if(k==0||nums.size()<2)
         //   return nums;
        reverse(nums.begin(),nums.begin()+nums.size()-k);
        reverse(nums.begin()+nums.size()-k,nums.end());
        reverse(nums.begin(),nums.end());
  //      return nums;
    }
};
```
## 2.存在重复
* 给定一个整数数组，判断是否存在重复元素。
如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。
```
示例 1:       
输入: [1,2,3,1]         
输出: true         
示例 2:          
输入: [1,2,3,4]    
输出: false       
示例 3:    
输入: [1,1,1,3,3,4,3,2,4,2]    
输出: true    
```

自己提交的代码：
```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        vector<int> temp;
        for(int i=0;i<nums.size();i++)
            temp.push_back(nums[i]);
        auto unique_end=unique(nums.begin(),nums.end());
        nums.erase(unique_end,nums.end());
        if(temp.size()!=nums.size())
            return true;
        else
            return false;
        
    }
};
//（<font color=#FF0000> 样例[1,2,3,1]总是出现逻辑判断错误 </font>）存在一点问题，暂未查找到。正在解决当中
```
---
```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        set<int> values;
        for (auto num : nums) {
            values.insert(num);
        }
        return nums.size() != values.size();
    }
};
//这里用到了STL标准库中对set()无重复特性的使用，简易、恰到好处。
```
---
```c++
class Solution {
public:
    /**
     * @param nums: the given array
     * @return: if any value appears at least twice in the array
     */
    bool containsDuplicate(vector<int> &nums) {
        // Write your code here
        unordered_set<int> dict;
        for(int num : nums) {
            if(dict.find(num) == dict.end())
                dict.insert(num);
            else
                return true;
        }
        return false;
    }
};
//用到了无序容器set，通过find()语句``(dict.find(num) == dict.end()``判断是否会添加重复元素。
```
## 3.找出只有一个的元素
* 给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。    
```
说明：
你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？
示例 1:
输入: [2,2,1]
输出: 1
示例 2:
输入: [4,1,2,1,2]
输出: 4
```
```c++
//根据消化的强大异或功能表现出来：
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        
        int result=0;
        for(int i:nums)
            result^=i;
        return result;
    }
};
//哈希集这种思路也值得借鉴！

若第一次出现，插入哈希集；
第二次出现，冲哈希集内删除；
最后剩下的就是那个只出现一次的数字。
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        unordered_set<int> bobo;
        int ans;
        for(auto i : nums){
            if(bobo.count(i))   bobo.erase(i);
            else    bobo.insert(i);
        }
        for(auto j : bobo)  ans = j;
        return ans;
    }
};
```
## 4.两个数组的交集 II
* 给定两个数组，编写一个函数来计算它们的交集。
```
示例 1:
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2,2]
示例 2:
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [4,9]
``` 
```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        
        vector<int>bobo;
        vector<int>::iterator it;
        for(auto i=0;i<nums1.size();i++)
        {             
            it=find(nums2.begin(),nums2.end(),nums1[i]);
            
            if(it!=nums2.end())
            {      
                bobo.push_back(nums1[i]);                                                                                                                                                 
                nums2.erase(it);
        }
        }
        
         return bobo;
    
}};
```
## 5.移动零
* 给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
```
示例:
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:必须在原数组上操作，不能拷贝额外的数组。尽量减少操作次数。
```
```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        
        if(count(nums.begin(),nums.end(),0)&&(count(nums.begin(),nums.end(),0)==nums.size()))
            return;
        
        vector<int>::iterator it=nums.begin();
     //   sort(nums.begin(),nums.end());      
        int i=0;
        
        do{
            if(nums[i]!=0){
           //     nums.erase(it);
           //     nums.push_back(0);
                it++;
                i++;
                }
            else{
                 nums.erase(it);
                 nums.push_back(0);
            }
      //     i++;
        }
        while(i<nums.size()-count(nums.begin(),nums.end(),0));
        return;
    }
};
//这段代码敲得比较爽，像是菜鸟在跟高手切磋（编译器）,我出一拳，他反打我，我又解决完锤回去。来来回回折腾挺久的，看到绿色的通过，心理倍儿开心。
之前代码的问题主要出在程序运行过程中超出限制，其原因多是下标或容器范围自己心中没计算好，要么造成泄露要么无限循环等，最终解决。
缺点程序不够精简，执行用时：432 ms。  
```
```c++
//解决单独的子问题，然后将它们组合在一起以得到最终的解决方案,这个应该想到的。
空间局部最优化/
void moveZeroes(vector<int>& nums) {
    int n = nums.size();

    // Count the zeroes
    int numZeroes = 0;
    for (int i = 0; i < n; i++) {
        numZeroes += (nums[i] == 0);
    }

    // Make all the non-zero elements retain their original order.
    vector<int> ans;
    for (int i = 0; i < n; i++) {
        if (nums[i] != 0) {
            ans.push_back(nums[i]);
        }
    }

    // Move all zeroes to the end
    while (numZeroes--) {
        ans.push_back(0);
    }

    // Combine the result
    for (int i = 0; i < n; i++) {
        nums[i] = ans[i];
    }
}
```
```c++
void moveZeroes(vector<int>& nums) {
    int lastNonZeroFoundAt = 0;
    // If the current element is not 0, then we need to
    // append it just in front of last non 0 element we found. 
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != 0) {
            nums[lastNonZeroFoundAt++] = nums[i];
        }
    }
    // After we have finished processing new elements,
    // all the non-zero elements are already at beginning of array.
    // We just need to fill remaining array with 0's.
    for (int i = lastNonZeroFoundAt; i < nums.size(); i++) {
        nums[i] = 0;
    }
}
//这个方法巧妙的多，实现了空间最优O（1）。现将非零元素以原始排序方式，拷贝至储存于数组前项；后以剩余元末尾补零的方式完成。可谓精妙！！！
```
# Share
分享一点刷力扣的经历吧，之前看到成功52期同学的历程，打心里还是蛮佩服的。刚看到容易的题目提支支吾吾、没有头绪，花很长世间都没有受益。一次次从其他同学分享的思路顺着里下来，说实话很没有成就感。一周一题的量显然对在校生过于宽松，慢慢把量增起来，从照着打、脑子里出现自己的蛮力算法到一步步试错，今天终于成功了一把，感觉不错，小有所成。继续吧、贵在坚持。
# Review
[How To Ask Questions The Smart Way](http://www.catb.org/~esr/faqs/smart-questions.html#writewell)文章比较长，还未读完。       
    中文书籍《提问是一门艺术》，之前有浏览过书名，但没深入了解。此篇文章更像是《提问的艺术》Geek版；文章介绍的非常详细，从如何仔细挑选自己领域的论坛，提问思考的方式，该如何可以训练自己的思维，如何正确的使用开源平台等等。    节选一些自己收获到的一些知识：    
    1.提问之前，搜寻论坛、Web、手册、FAQ、检测和实验数据、身边同学、开源平台。         
    2.所要搜寻的答案质量会取决于你提问的角度和深度。在做哪怕一点细微小事，如果自己还有没找到问题，继续坚持自己思考，不过大脑的提问所得到的受益甚小/真正能解决问题的人是不看或者不想浪费时间在这些没过脑的提问上面。
    3.文中提出了一个让我眼前一亮的方法：使用有意义、具体的语言来描述标题。“object - deviation”，字面反过来是对象-偏差（即是差异），“对象”部分指定什么东西或一组东西有问题，“偏差”部分描述与预期行为的偏差；这样显著的提高了提问的效率，而且描述问题清晰。     
    4.同样，在开源平台上永远不要一味地做一位索取者。是虽然你的问题，error or warning 已经有太多的类似问题无需再次开帖，但是通过自己的亲身实践去解决一些力所能及的提问同样也能实现自己的价值，帮助他人提高自己。
# Tip
   * 在敲打C++primer习题时出现。在输入流作为for语句的判断条件时，如何使之停止？    windows按ctrl + z，linux按ctrl + d
