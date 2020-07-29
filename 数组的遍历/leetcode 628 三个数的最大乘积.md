# leetcode 628 三个数的最大乘积

## 排序的方法

```c
int maximumProduct(int* nums, int numsSize){
//不能只找前三大的数，要分情况。1.全正数,全负数或只有一个负数，前三大的数的乘积即为答案。2.有两个或以上个负数，也有正数，两个最小负数相乘与第二三大的数相乘相比，大的那个乘最大的数即为答案。
    for(int i=0;i<numsSize;i++)
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
        }
    if(nums[0]>0||nums[numsSize-1]<0||(nums[0]<0&&nums[1]>0))
    {
        return nums[numsSize-1]*nums[numsSize-2]*nums[numsSize-3];
    }
    else
    {
        int p,q;
        p=nums[0]*nums[1];
        q=nums[numsSize-2]*nums[numsSize-3];
        if(p>q)
        {
            return p*nums[numsSize-1];
        }
        else
        {
            return  q*nums[numsSize-1];
        }
    }
}
```

出现的问题：当数组大时，超出时间限制

## 不排序的方法

```c
int maximumProduct(int* nums, int numsSize){
//不排序的方法，找出最大的三个数和最小的两个数，再按情况进行分析
    int first,second,third,min,mins;
    // 找出最大的三个数
    for(int i=0;i<3;i++)
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
        }
    //必须先把这三个数装到first,second,third里，才能按冒泡排序法找最小的两个数，否则当数组比较小时，会出现一个数既是第三大又是第二小，此时，这个数的位置就会与预期不同
        first =nums[numsSize-1];
        second=nums[numsSize-2];
        third =nums[numsSize-3];
    //找出最小的两个数，也是使用冒泡排序的方法求，要注意，也是把小的数沉到数组的最后面
    for(int i=0;i<2;i++)
        {
            for(int j=0;j<numsSize-i-1;j++)
            {
                if(nums[j]<nums[j+1])
                 {   
                    int temp=nums[j];
                    nums[j]=nums[j+1];
                    nums[j+1]=temp;
                }
            }
        }
    min=nums[numsSize-1];
    mins=nums[numsSize-2];
    if(min*mins>third*second)
    {
        return min*mins*first;
    }
    else
    {
        return third*second*first;
    }
}

```

