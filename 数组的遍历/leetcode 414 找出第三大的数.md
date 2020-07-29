# leetcode 414 找出第三大的数

错误版本：


```c
int thirdMax(int* nums, int numsSize){
    int q;
    if(numsSize<3)
    {
        q=numsSize;
    }
    else
    {
        q=3;
    }
    for(int i=0;i<q;i++)
    {
        for(int j=0;j<numsSize-i-1;j++)
        {
            if(nums[j]>nums[j+1])
           {
                int temp=nums[j];
                nums[j]=nums[j+1];
                nums[j+1]=temp;
           }
        }
        if(i>0&&nums[numsSize-i]==nums[numsSize-i-1])
        {
            nums[numsSize-i-1]=-2147483648;
            i--;
        }
    }
    if(numsSize<3)
    {
        return nums[numsSize-1];
    }
    else
    {
        if(nums[numsSize-3]==-2147483648)
        {
            return nums[numsSize-1];
        }
        else
        {
             return nums[numsSize-3];
        }
    }

}
```

此版本易出现的问题：1. 可能出现的情况过多，很难考虑周全，[1,2] , [1,1,-2147483648] , [1,2,-2147483648] 容易出现不正确的结果。 2.易超时

> -2147483648为int范围内最小的数

可改进的方案：

​		1. 直接找出first，second，third来讨论。

​		2.先找到最大值与最小值，然后将数列中所有的最大值换成最小值，这里用j来计重复的个数。然后此时再去寻找新数列里的最大值，这个最大值就是原数列的第二大的值，再把现在数列里的最大值全部换为最小值后，再去找最大值，此时的最大值便是最初数列的第三大的值。

