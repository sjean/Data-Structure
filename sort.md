# 数据结构与算法

#### 1. 排序算法

##### 插入类排序：
**1. 直接插入排序**
	  思想：最基本的插入排序，将第i个插入到前i-1个中的适当位置。
 时间复杂度：T(n) = O(n²)。
 空间复杂度：S(n) = O(1)。
稳定性：稳定排序。循环条件while(r[0].key < r[j].key)保证的。

```
void InsSort(RecordType r[], int length)  
{  
    for(i = 2; I <= length; i++)  
    {  
        r[0] = r[i];  
        j = i – 1;  
        while(r[0].key < r[j].key)  
        {  
            r[j + 1] = r[j]; j = j – 1;  
        }  
        r[j+1] = r[0];  
    }  
}  
```

**2. 折半插入排序**
  思想：因为是已经确定了前部分是有序序列，所以在查找插入位置的时候可以用折半查找的方法进行查找，提高效率。
 时间复杂度：比较时的时间减为O(n㏒n)，但是移动元素的时间耗费未变，所以总是得时间复杂度还是O(n²)。
 空间复杂度：S(n) = O(1)。
  稳定性：稳定排序。

```
  void BinSort(RecordType r[], int length)  
{  
    for(i = 2; i <= length; i++)  
    {  
        x = r[i];  
        low = 1; high = i – 1;  
        while(low <= high)  
        {  
            mid = (low + high) / 2;  
            if(x.key < r[mid].key)  
                high = mid – 1;  
            else  
                low = mid – 1;  
        }  
        for(j = i – 1; j >= low; --j)  
            r[j + 1] = r[j];  
        r[low] = x;  
    }  
}  
```

**3. 希尔排序**
 ①   思想：又称缩小增量排序法。把待排序序列分成若干较小的子序列，然后逐个使用直接插入排序法排序，最后再对一个较为有序的序列进行一次排序，主要是为了减少移动的次数，提高效率。原理应该就是从无序到渐渐有序，要比直接从无序到有序移动的次数会少一些。
②   时间复杂度：O(n的1.5次方)
③   空间复杂度：O(1)
④   稳定性：不稳定排序。{2,4,1,2}，2和1一组4和2一组，进行希尔排序，第一个2和最后一个2会发生位置上的变化。

```
void ShellInsert(RecordType r[], int length, int delta)  
{  
    for(i = 1 + delta; i <= length; i++)/*1+delta为第一个子序列的第二个元素的下表*/  
    if(r[i].key < r[1 - delta].key)  
    {  
        r[0] = r[i];  
        for(j = i – delta; j > 0 && r[0].key < r[j].key; j -=delta)  
            r[j + delta] = r[j];  
        r[j + delta] = r[0];  
    }  
}  
void ShellSort(RecordType r[], int length, int delta[], int n)  
{  
    for(i = 0; i <= n – 1; ++i)  
        ShellInsert(r, length, delta[i]);  
}  
```

##### 交换类排序：
**1、  冒泡排序：**
①   思想：反复扫描待排序序列，在扫描的过程中顺次比较相邻的两个元素的大小，若逆序就交换位置。第一趟，从第一个数据开始，比较相邻的两个数据，（以升序为例）如果大就交换，得到一个最大数据在末尾；然后进行第二趟，只扫描前n-1个元素，得到次大的放在倒数第二位。以此类推，最后得到升序序列。如果在扫描过程中，发现没有交换，说明已经排好序列，直接终止扫描。所以最多进行n-1趟扫描。
②   时间复杂度：T(n) = O(n²)。
③   空间复杂度：S(n) = O(1)。
④   稳定性：稳定排序。

```
void BubbleSort(RecordType r[], int length)  
{  
    n = length;  
    change = TRUE;  
    for(i = 1; i <= n – 1 && change; i++)  
    {  
        change = FALSE;  
        for(j = 1; j <= n – I; ++j)  
            if(r[j].key > r[j + 1].key)  
            {  
                x = r[j];  
                r[j] = r[j + 1];  
                r[j + 1] = x;  
                change = TRUE;  
             }  
    }  
}  
```
**2、  快速排序：**
①   思想：冒泡排序一次只能消除一个逆序，为了能一次消除多个逆序，采用快速排序。以一个关键字为轴，从左从右依次与其进行对比，然后交换，第一趟结束后，可以把序列分为两个子序列，然后再分段进行快速排序，达到高效。
②   时间复杂度：平均T(n) = O(n㏒n)，最坏O(n²)。
③   空间复杂度：S(n) = O(㏒n)。
④   稳定性：不稳定排序。{3， 2， 2}

```
void QKSort(RecordType r[], int low, int high)  
{  
    int pos;  
    if(low < high)  
    {  
        pos = QKPass(r, low, high);  
        QKSort(r, low, pos - 1);  
        QKSort(r, pos + 1, high);  
    }  
}  
int QKPass(RecordType r[], int left, int right)  
{  
    RecordType x;  
    int low, high;  
    x = r[left];  
    low = left;  
    high = right;  
    while(low < high)  
    {  
        while(low < high && r[high].key >= x.key)  
            high--;  
        if(low < high)  
        {  
            r[low] = r[high];  
            low++;  
        }  
        while(low < high && r[low].key < x.key)  
            low++;  
        if(low < high)  
        {  
            r[high] = r[low];  
            high--;  
        }  
    }  
    r[low] = x;  
    return low;  
}  
```

##### 选择类排序：
**1、  简单选择排序：**
①   思想：第一趟时，从第一个记录开始，通过n – 1次关键字的比较，从n个记录中选出关键字最小的记录，并和第一个记录进行交换。第二趟从第二个记录开始，选择最小的和第二个记录交换。以此类推，直至全部排序完毕。
②   时间复杂度：T(n) = O(n²)。
③   空间复杂度：S(n) = O(1)。
④   稳定性：不稳定排序，{3， 3， 2}。

```
void SelectSort(RecordType r[], int length)  
{  
    n = length;  
    for(i = 1; i <= n - 1; i++)  
    {  
        k = i;  
        for(j = i + 1; j <= n; i++)  
        if(r[j].key < r[k],key)  
            k = j;  
            if(k != i)  
            {  
                x = r[i];  
                r[i] = r[k];  
                r[k] = x;  
            }  
    }  
}  
```
**2、  堆排序：**
①   思想：把待排序记录的关键字存放在数组r[1…n]中，将r看成是一刻完全二叉树的顺序表示，每个节点表示一个记录，第一个记录r[1]作为二叉树的根，一下个记录r[2…n]依次逐层从左到右顺序排列，任意节点r[i]的左孩子是r[2i]，右孩子是r[2i+1]，双亲是r[i/2向下取整]。然后对这棵完全二叉树进行调整建堆。
②   时间复杂度：T(n) = O(n㏒n)。
③   空间复杂度：S(n) = O(1)。
④   稳定性：不稳定排序。{5， 5， 3}

```
(1)调整堆：
void sift(RecordType r[], int k, int m)  
{  
    /*假设r[k...m]是以r[k]为根的完全二叉树，而且分别以r[2k]和r[2k+1]为根的左右子树为大根堆，调整r[k]，使整个序列r[k...m]满足堆的性质*/  
    t = r[k];/*暂存“根”记录r[k]*/  
    x = r[k].key;  
    i = k;  
    j = 2 * i;  
    finished = FALSE;  
    while(j <= m && !finished)  
    {  
        if(j < m && r[j].key < r[j + 1].key)  
            j = j + 1;/*若存在右子树，且右子树根的关键字大，则沿右分支“筛选”*/  
        if(x >= r[j].key)  
            finished = TRUE;/*筛选完毕*/  
        else  
        {  
            r[i] = r[j];  
            i = j;  
            j = 2 * i;  
        }/*继续筛选*/  
    }  
    r[i] = t;/*将r[k]填入到恰当的位置*/  
}  

(2)建初堆：
void crt_heap(recordType r[], int length)  
{  
    n = length;  
    for(i = n / 2; i >= 1; --i)/*自第n/2向下取整 个记录开始进行筛选建堆*/  
        sift(r, i, n);  
}  

(3)堆排序：
void HeapSort(RecordType r[], int length)  
{  
    crt_heap(r, length);  
    n = length;  
    for(i = n; i >= 2; --i)  
    {  
        b = r[1];/*将堆顶记录和堆中的最后一个记录互换*/  
        r[1] = r[i];  
        r[i] = b;  
        sift(r, 1, i - 1);/*进行调整，使r[1…i-1]变成堆*/  
    }  
}  
```


##### 归并排序：
①   思想：假设初始序列右n个记录，首先将这n个记录看成n个有序的子序列，每个子序列的长度为1，然后两两归并，得到n/2向上取整 个长度为2（n为奇数时，最后一个序列的长度为1）的有序子序列。在此基础上，在对长度为2的有序子序列进行两两归并，得到若干个长度为4的有序子序列。如此重复，直至得到一个长度为n的有序序列为止。
②   时间复杂度：T(n) = O(n㏒n)。
③   空间复杂度：S(n) = O(n)。
④   稳定性：稳定排序。

```
void Merge(RecordType r1[], int low, int mid, int high, RecordType r2[])  
{  
    /*已知r1[low...mid]和r1[mid + 1...high]分别按关键字有序排列，将它们合并成一个有序序列，存放在r2[low...high]*/  
    i = low;  
    j = mid + 1;  
    k = low;  
    while((i <= mid) && (j <= high))  
    {  
        if(r1[i].key <= r1[j].key)  
        {  
            r2[k] = r1[i];  
            ++i;  
        }  
        else  
        {  
            r2[k] = r1[j];  
            ++j;  
        }  
        ++k;  
    }  
    while(i <= mid)  
    {  
        r2[k] = r1[i];  
        k++;  
        i++;  
    }  
    while(j <= high)  
    {  
        r2[k] = r1[j];  
        k++;  
        j++;  
    }  
}  
void MSort(RecordType r1[], int low, int high, RecordType r3[])  
{  
    /*r1[low...high]经过排序后放在r3[low...high]中，r2[low...high]为辅助空间*/  
    RecordType r2[N];  
    if(low == high)  
    r3[low] = r1[low];  
    else  
    {  
        mid = (low + high) / 2;  
        MSort(r1, low, mid, r2);  
        MSort(r1, mid + 1, high, r2);  
        Merge(r2, low, mid, high, r3);  
    }  
}  
void MergeSort(RecordType r[], int n)  
{  
    /*对记录数组r[1...n]做归并排序*/  
    MSort(r, 1, n, r);  
}  
```
