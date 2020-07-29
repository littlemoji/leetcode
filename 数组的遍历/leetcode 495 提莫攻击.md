# leetcode 495

```c
long int findPoisonedDuration(int* timeSeries, int timeSeriesSize, int duration){
    long int PoisonedDuration=0;
    for(int i=0;i<timeSeriesSize-1;i++)
    {
        int j=i+1;
        if(timeSeries[j]-timeSeries[i]>=duration)
        {
            PoisonedDuration=PoisonedDuration+duration;
        }
        else
        {
            PoisonedDuration=PoisonedDuration+timeSeries[j]-timeSeries[i];
        }
    }
    if(timeSeriesSize>0)
    {
         PoisonedDuration=PoisonedDuration+duration;
    }
    return PoisonedDuration;
}
```

