# leetcode 645 在集合中找出重复和确实的元素

> 第一次用python写题目，遇到了很多很多很多。。。问题 :crying_cat_face:

题目描述：

+ 集合 S 包含从1到 n 的整数。不幸的是，因为数据错误，导致集合里面某一个元素复制了成了集合里面的另外一个元素的值，导致集合丢失了一个整数并且有一个元素重复。

+ 给定一个数组 nums 代表了集合 S 发生错误后的结果。你的任务是首先寻找到重复出现的整数，再找到丢失的整数，将它们以数组的形式返回。

示例 1:

+ 输入: nums = [1,2,2,4]
  输出: [2,3]

注意:

+ 给定数组的长度范围是 [2, 10000]。
+ 给定的数组是无序的。



解题思路

1. 找出集合中重复出现的整数： 从头扫到尾，只要当前元素值与下标不同，就做一次判断,nums[i-1]与nums[nums[i-1]-1]， 相等就认为找到了重复元素，返回true,否则就交换两者，继续循环。直到最后还没找到认为没找到重复元素。 （这里的-1是由于集合是从1开始，而列表是由0开始）

    https://blog.csdn.net/weixin_42712658/article/details/99685526 

2. 找出丢失的整数：使用while循环（1~n），判断每个整数是否都在集合。`if n not in nums`，如果不在，返回fault，记录。



解题过程中遇到的知识点

1. python中的while和for循环

    https://www.runoob.com/python/python-while-loop.html 

    https://www.runoob.com/python/python-for-loop.html 

    https://www.cnblogs.com/zxy6/p/11606194.html 

2. python列表的简单操作

    https://www.runoob.com/python/python-lists.html 





解题过程中遇到的报错

1.  Unbound Local Error: local variable 'XX' referenced before assignment 

   大意：   本地变量XX引用前没定义。 

   错误原因： 在于python没有变量的声明 , 所以它通过一个简单的规则找出变量的范围 ：如果有一个函数内部的变量赋值 ，该变量被认为是本地的，所以如果有修改变量的值就会变成局部变量。 

   解决方法：在变量前加上“global“关键字来说明该变量是全局变量

2. Type Error : 'XX' object does not support XXX assignment

   大意： XX这个实例不支持或不能分配给XXX类型。 

   错误原因：类型不匹配

   

错误版本

```python
class Solution(object):
    def findErrorNums(self, nums):
         n=1
         error=[]
         while n<=len(nums):
            if n!=nums[n-1]:
                if nums[n-1]==nums[nums[n-1]-1]:
                    error.append(nums[n-1])
                else:
                    nums[n-1],nums[nums[n-1]-1]=nums[nums[n-1]-1],nums[n-1]
            if n not in nums:
                error.append(n)
            n+=1
         return error
```

