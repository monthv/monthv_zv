## 排序

#### 冒泡排序

```c#
public static void BubbleSort(this int[] arry)
        {
            for (int i = 0; i < arry.Length; i++)
            {
                for (int x = 0; x < arry.Length-1-i; x++)
                {
                    if (arry[x]>arry[x+1])
                    {
                        int temp = arry[x];
                        arry[x] = arry[x + 1];
                        arry[x + 1] = temp; 
                    }
                }
            }
            arry.ToList().ForEach(item =>
            {
                Console.WriteLine(item);
            });
        }
```

#### 选择排序

```c#
public static void SelectionSort(this int[] arry)
        {
            for (int i = 0; i < arry.Length - 1; i++)
            {
                //记录最小值索引
                int minIndex = i;
                for (int j = i + 1; j < arry.Length; j++)
                {
                    if (arry[j] < arry[minIndex])
                    {
                        minIndex = j;
                    }
                }
                //交互最小值 : 当前索引就是最小值时就不用交换
                if (minIndex != i)
                {
                    int temp = arry[i];
                    arry[i] = arry[minIndex];
                    arry[minIndex] = temp;
                }
            }
            arry.ToList().ForEach(item =>
            {
                Console.WriteLine(item);
            });
        }
```

## 递归

```c#
 static int Recursion(int n)//
        {
            //在方法中判断n是否为1或者2如果是返回1
            if(i<=0)
            {
                return 0;
            }
            else if(i>0 && i<=2)
            {
                return 1;
            }
            //如果不是返回斐波那契公式重新调用自己直到求出所要值
            return Recursion(i - 2) + Recursion(i - 1);
        }
```

## 计算1-2+3-4+...+M

```mssql
 //通过奇偶性    
   static int Man(int m)    
   {    
       int sum = 0;    
       for (int i = 1; i <= m; i++)    
       {    
           if (i % 2 >0)  //即为奇数    
               sum += i;    
           else    
               sum -= i;    
       }    
       return sum;    
   }  
```

