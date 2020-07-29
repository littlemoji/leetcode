# leetcode 485 最长1串的个数

```c
int findMaxConsecutiveOnes(int* nums, int numsSize){
    int n[numsSize]; //n数组用于存放连续1的个数
    int j=0, q=0; //q用于指向n数组，j用于计算1的个数
    //计算每一串1的长度
    if(nums[0]==1)
    {
        j=1;
        n[q]=1;
    }
    for(int i=1;i<numsSize;i++)
    {
        if(nums[i]==1)
        {
            j++;
            n[q]=j;
            if(i==numsSize-1)
            {
                q++;
            }
        }
        if(nums[i]==0&&nums[i-1]==1)
        {
            n[q]=j;
            j=0;
            q++;
        }
    }
    //求n数组中最大的数即题目所求
    int max=0;
    //特殊情况
    if(q==0&&nums[0]==1)
    {
        max=1;
    }
    for(int i=0;i<q;i++)
    {
        if(n[i]>max)
        {
            max=n[i]; 
        }
    }
return max;
}
//每一个0就是一个段
//若是使用上面的方法，则每次修改一串1的个数都需存到数组中，防止最后的数字是1，无法存到数组中
//代码改进：无需把一串1个数存在一个数组中再去比较，可以直接在计算的时候进行比较，可以省去甚多麻烦
```

