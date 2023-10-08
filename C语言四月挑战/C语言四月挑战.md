# 第零天 平时积累

## 0.1 判断一个数是否是质素

- 质素的定义
  - 一个数只能被自己本身和一整除，那么该数就是质数。
  - 注意0，1不是质素；
- 当一个数不是质数时，必定存在两个约数，一个大于等于sqrt(n)，**另一个小于sqrt(n)**。利用这种特性，可以对方法1进行改进，只判断数n能否被小于sqrt(n)的数整除。

![img](.\Images\质数1.png)

在寻找一个数 num是否为质数时，你只需要测试是否存在小于等于 num 的平方根的因子。因为如果一个数有一个大于其平方根的因子，那么它必定也有一个小于等于其平方根的因子，因此只需要测试平方根以下的数是否能整除 num。

实例代码：

```java
public static boolean isPrime(int n) {
    if (n <= 3) {
        return n > 1;
    }
    //判断一个数能否被小于sqrt(n)的数整除
    int sqrt = (int)Math.sqrt(n);
    for (int i = 2; i <= sqrt; i++) {
        if(n % i == 0) {
            return false;
        }
    }
    return true;
}
```

对不等式两边开方为：

```java
public static boolean isPrime(int n) {
    if (n <= 3) {
        return n > 1;
    }
    for (int i = 2; i * i <= n; i++) {
        if(n % i == 0) {
            return false;
        }
    }
    return true;
}
```

## 0.2 分块算法

- 寻求一个0~1000以内的质素，采用多进程和分块算法实现。
- 分块算法核心是，0~200分给进程1, 201~400分给进程2..........

## 0.3 交叉分配算法

- 寻求一个0~1000以内的质素，采用多进程和交叉分配算法实现。
- 交叉分配算法核心是: 假设有10个进程，1号进程算第一位，2号进程算第二位，3号进程算第三位........; 依次这样重复

## 0.4 池内算法



# 第1天 数组中出现一次的数字

> 操作数组时；
>
> 可以将数组看做两个
>
> ​	[2, 1, 2]

​		^

> i = 0, 1, 2
>
> ​	[2, 1, 2]
>
> ​	 ^
>
> j = 0, 1, 2
>
> 
>
> i = 0时；
>
> j = 0, 1, 2
>
> 
>
> i = 1时；
>
> j = 0, 1, 2
>
> 
>
> i = 2时；
>
> j = 0, 1, 2
>
> 



## c语言实现正常实现

```c
#include <iostream>

using namespace std;

int singleNum(const int *arr, int length){
    if(arr == nullptr) return -1;

    for(int i = 0; i < length; i++){
        int count = 0;
        for(int j = 0; j < length; j++){
            if(arr[i] == arr[j]){
                count++;
            }
        }
        if(count == 1){
            return arr[i];
        }
    }
    return 0;
}

int main() {
    // 定义一个数组
    int arr[] = {2, 2, 4, 5, 7, 5, 7};
    int data, length = sizeof (arr)/sizeof (arr[0]);

    data = singleNum(arr, length);
    cout<<data<<endl;       // 输出4
    return 0;
}
```

## 异或实现

- 异或最基础的用法就是判断是否有重复数字出现；
- 异或最通俗的理解就是算术加法；

**需要注意的是：回圈是从第2个元素开始。我犯错了；**

```c
#include <iostream>

using namespace std;

int singleNum(const int *arr, int length){
    if(arr == nullptr) return -1;
    int onData = arr[0];

    //onData = arr[0] + arr[1] + arr[2] + …… + arr[i];
    for(int i = 1; i < length; i++){
        onData ^=  arr[i];
    }
    return onData;
}

int main() {
    // 定义一个数组
    int arr[7] = {2, 2, 4, 5, 7, 5, 7};
    int data;
    int length = sizeof (arr)/sizeof (arr[0]);

    data = singleNum(arr, length);
    cout<<data<<endl;       // 输出4
    return 0;
}
```

## C++实现

```c++
#include <iostream>
#include <vector>

using namespace std;

class Solve {

public:
    static int method(vector<int> &nums, int target) {
        // 定义两个指针
        int left = 0;
        int right = nums.size() - 1;

        // 数组内只有一个元素的特殊情况，所以要是 <=
        while (left <= right) {
            int midden = left + ((right - left) / 2);
            if (nums[midden] < target) {
                right = midden - 1;
            } else if (nums[midden] > target) {
                left = midden + 1;
            } else {
                return midden + 1;
            }
        }
        // 都没找到，就返回 -1；
        return -1;
    }
};


int main(int argc, char *argv[]) {
    vector<int> array{12, 45, 1, -6, 7, 8, 2, 7};

    int result = Solve::method(array, -6);
    cout << "结果为：" << result << endl;
}
```

# 第2天 将一个数拆分为个十百千位

### 取数算法

```c
#include <cstdio>
#include <climits>

void method2();

void method3();

int main() {

    method3();
}

void method0(){
    // 求取整形数据的最大值
    // #include <limits.h>
    printf("%d\n", INT_MAX);
}

int method1() {
    int num = 54321;

    // 取出最后一位   d1 = 1
    int d1 = num % 10;

    // 去除最后一位，然后取出末尾一位   da = 2;
    int d2 = num / 10 % 10;

    // 去除最后两位，然后取出末尾一位   d3 = 3
    int d3 = num / 100 % 10;

    // 去除最后一位，然后取出末尾一位   d4 = 4;
    int d4 = num / 1000 % 10;

    // 去除最后两位，然后取出末尾一位   d5 = 5
    int d5 = num / 10000 % 10;
    return -1;
}

void method2() {
    int num = 3579491, m = 1;
    for (char count = 1; count <= 10; count++) {
        int result = num / m % 10;
        if (count < 10) {
            m *= 10;
        }
        printf("%d\n", result);
    }
}

void method3() {
    int num = 21219849;

    // 判断整形数据是否为零
    while (num != 0) {

        // 取出末尾数
        int result = num % 10;

        printf("%d\n", result);

        // 每次都将整形数据去除末尾一位
        num /= 10;
    }
}
```



### 快乐数

```c
#include <cstdio>

int method0(int n);
bool contains(const int *array, int arrayLength, int n);
int isHappy(int n);


int main() {
    int n = 19;

    printf("%d\n", isHappy(n));
}
/*
 * 将一个数取出每个位的具体数据，进行操作
 * n = 45824
 * d1 = 4, d2 = 2, d3 = 8, d5 = 5, d6 = 4;
 * result = 4*4 + 2*2 + 8*8 + 5*5 + 4*4 = 3564;
 *
 * n = result;
 * d1 = .....;
 * */
int method0(int n) {
    if (0 == n) {
        return -1;
    }
    int result = 0;

    while (0 != n) {

        // 取出每一位的数据
        int d = n % 10;
        //printf("%d\n", d);
        n /= 10;

        // 将取出的数据 平方后相加
        result += d * d;
    }
    return result;
}

/*
 * 判断一个数在数组中是否出现过
 * 参数1：数组
 * 参数2：数组长度
 * 参数3：需要判断的数字*/
bool contains(const int *array, int arrayLength, int n){
    if(array == nullptr || arrayLength <= 0)
        return false;
    for(int i = 0; i < arrayLength; i++){
        if(array[i] == n){
            return true;
        }
    }
    return false;
}

/*
 * 方法一：
 * 利用数组进行判断，判断数组中是否有重复出现的数字*/
int isHappy(int n){
    int history[1000];
    int size = 0;

    /*
     * 检测数据是否在数组中是否出现过*/
    while(!(contains(history, 1000, n))){

        // 将数据存入带数组中
        history[size] = n;

        // 数组内部区域进行移位
        size++;

        // 获取数据
        n = method0(n);
    }
    if(n==1){
        return 1;
    }
    return 0;
}
```

# 第3天 最大子数组

```c++
#include <cstdio>

int method(const int *array, int arrayLength);
int method2(const int *array, int arrayLength);

int main() {
    int array[] = {2, -4, -5, 6, 7, -6, 5, 1};
    int arrayLength = sizeof (array)/sizeof(array[0]);

    int result = method2(array, arrayLength);
    printf("最大值为：%d\n", result);
    return 0;
}

int method(const int *array, int arrayLength) {
    if (array == nullptr || arrayLength == 0) {
        return -1;
    }
    /*
     * 定义起点和终点
     * 起点i从数组的第零个数据开始，
     * j从第i的位置开始*/
    volatile int i, j;

    // 目前位置，最大的值假设为第一个数
    int max = array[0];

    for (i = 0; i < arrayLength; i++) {       // i: 0, 1, 2, 3, ... , arrayLength - 1;
        for (j = i; j < arrayLength; j++) {  // j: i, ... , arrayLength - 1;

            // 定义一个数，该数从i的位置一直 数 到j的位置
            // sum = 0 + array[i] + ... + array[j]
            volatile int sum = 0;
            for (int k = i; k <= j; k++) {      // k: i ~ j;
                sum += array[k];
            }
            printf("sum = %d\n",sum);
            // 如果新来的数比原本的数还要大，那么就更新原来的数。
            if (sum > max) {
                max = sum;
            }
        }
    }
    return max;
}

// 对方法一进行优化
int method2(const int *array, int arrayLength){
    if (array == nullptr || arrayLength == 0) {
        return -1;
    }
    /*
     * 定义起点和终点
     * 起点i从数组的第零个数据开始，
     * j从第i的位置开始*/
    volatile int i, j;

    // 目前位置，最大的值假设为第一个数
    int max = array[0];

    for (i = 0; i < arrayLength; i++) {       // i: 0, 1, 2, 3, ... , arrayLength - 1;

        int sum = 0;
        for (j = i; j < arrayLength; j++) {  // j: i, ... , arrayLength - 1;

            // 定义一个数，该数从i的位置一直 数 到j的位置
            // sum = sum + array[j];
            sum += array[j];

            printf("sum = %d\n",sum);
            // 如果新来的数比原本的数还要大，那么就更新原来的数。
            if (sum > max) {
                max = sum;
            }
        }
    }
    return max;
}
```

# 第4天 移动零数字

## 交换两个数的位置

==任何多大的数组都能实现；==

```c
    int array[] = {12, 0};
    int arrayLength = sizeof (array)/sizeof(array[0]);
    /*
     * j: 取值范围 [0, arrayLength - 1];
     * 但是注意: 当 j = arrayLength - 1 时，不会在进入循环内;
     *  可以理解为：j取值范围[0, arrayLength - 1)
     * */
    for (int j = 0; j < arrayLength - 1; j++) {

        //printf("%d:%d \t", j, array[j]);
        array[j] = array[j] ^ array[j + 1];
        array[j + 1] = array[j] ^ array[j + 1];
        array[j] = array[j] ^ array[j + 1];
    }

// 交换后的数组为：array[] = {0, 12}

```

## 移动零数字

```c
#include <cstdio>

void method(int *array, int arrayLength);

int main() {

    int array[] = {12, 0, 4, 0, 7, 8, 0, 7, 4};
    int arrayLength = sizeof(array) / sizeof(array[0]);

    method(array, arrayLength);

    for (int j = 0; j < arrayLength; j++) {

        printf("%d:%d \t", j, array[j]);
    }
    printf("\n");
    return 0;
}

void method(int *array, int arrayLength) {
    if (array == nullptr || arrayLength == 0 || arrayLength == 1) {
        return;
    }
    while (true) {
        bool isFlag = true;
        for (int i = 0; i < arrayLength - 1; i++) {
            if (array[i] == 0 && array[i + 1] != 0) {
                isFlag = false;
                array[i] = array[i] ^ array[i + 1];
                array[i + 1] = array[i] ^ array[i + 1];
                array[i] = array[i] ^ array[i + 1];
            }
        }
        if (isFlag) {
            break;
        }
    }
}
```

# 第5天  数组谜



帮助记忆

```c
当传递的是 [0, 2, 45, 7] 由于只有一个矩阵,所以是一个*，矩阵内是数字；所以接受用 int *;

当传递的是["abc", "efg", "abg"] 由于只有一个矩阵，所以是一个*；矩阵内是char *，所以接受用 char **;

当传递的是[[1, 5, 7], [4, 7], [23]] 由于只有二个矩阵，所以是一个**；第二个矩阵也就是内部矩阵内是数字，所以接受用int **;

当传递的是[["abc", "efg", "abg"], ["efg", "dfg"], ["23"]] 由于只有二个矩阵，所以是一个**；第二个矩阵也就是内部矩阵内是char *；所以接受用char ***;
```

## 一维字符数组

```c
#include <stdio.h>
#include <stdlib.h>

/*
 * 用char **来接收 
 * */
void func(char **pString) {
    for(int i = 0; i < 3; i++){
        printf("%s\n", *(pString + i));
    }
}

int main(){
    char *arr[] = {"af", "cd", "ef"};
    func(arr);
    exit(0);
}
```

## 二维字符数组

```c
#include <stdio.h>
#include <stdlib.h>

void func(char ***strings, int num_arrays, int *array_sizes) {
    // 遍历并打印每个子数组中的字符串
    for (int i = 0; i < num_arrays; i++) {
        printf("Array %d:\n", i + 1);
        for (int j = 0; j < array_sizes[i]; j++) {
            printf("  String %d: %s\n", j + 1, *(*(strings + i) + j));
        }
    }
}

int main() {
    // 定义一个包含三个数组的数组
    char strings[][3][4] = {
            {"abc", "bcd", "rfd"},
            {"dfb", "adv"},
            {"efg"}
    };

    int num_arrays = sizeof(strings) / sizeof(strings[0]);
    int array_sizes[] = {3, 2, 1};

    // 将数组及其相关信息传递给函数

    char ***dynamic_strings = malloc(num_arrays * sizeof(char **));
    if (dynamic_strings == NULL) {
        perror("Memory allocation failed");
        return 1;
    }

    for (int i = 0; i < num_arrays; i++) {
        dynamic_strings[i] = malloc(array_sizes[i] * sizeof(char *));
        if (dynamic_strings[i] == NULL) {
            perror("Memory allocation failed");
            return 1;
        }

        for (int j = 0; j < array_sizes[i]; j++) {
            dynamic_strings[i][j] = strings[i][j];
        }
    }

    func(dynamic_strings, num_arrays, array_sizes);

    // 释放动态分配的内存
    for (int i = 0; i < num_arrays; i++) {
        free(dynamic_strings[i]);
    }
    free(dynamic_strings);

    return 0;
}
```



## 数组的基础知识

数组的存在，目的是用来存放相同的数据；

方式一：

```c
#include <stdio.h>
#include <stdlib.h>

//void func(int array[]){
void func(int *array){
}

int main(){
    int arr[] = {12, 45, 78};

    // 数组是不能直接进行复制的
    // int arr2[] = arr;

    // 或者
    // arr2 = arr;

    // 但是可以传递
    /*
     *  其实是实现了复制    int array[] = arr;
     *  arr其实是指针，指向第一元素；所以func() 传递的其实是一个地址；
     *  那么函数可以被修改为：
     *  void func(int *array)*/
    func(arr);

    for(int i = 0; i < 3; i++){
        printf("%d\n", arr[i]);			// 输出结果12 45 78 
    }
    exit(0);
}
```

方式二：

```c
#include <stdio.h>
#include <stdlib.h>

//void func(int array[]){
void func(int *array){
    array[0] = array[1] = array[2] = 0;
}

int main(){
    int arr[] = {12, 45, 78};

    func(arr);

    for(int i = 0; i < 3; i++){
        printf("%d\n", arr[i]);             // 输出结果为： 0 0 0
    }
    exit(0);
}
```

方式三：

```c
#include <stdio.h>
#include <stdlib.h>



int main(){
    // 定义一个字符串
    char str[12] = "hello world";
    const char *string = "Hello World";
    printf("%s\n", str);             // 输出结果为： hello world
    printf("%s\n", string);             // 输出结果为： Hello World
    
    exit(0);
}
```



# 第6天



# 第7天 Counting Elements

## c语言实现

```c
#include <iostream>


using namespace std;

int method(int *arr, int length);

int main() {
    int data;
    // 创建一个数组
    int arr[] = {1, 2, 4, 3, 5, 5, 7, 7};
    data = method(arr, sizeof(arr) / sizeof(arr[0]));
    cout<<data<<endl;
    exit(0);
}

/*
 * 给定一个原始数组，
 * 创建一个新数组plus1,plus1中的元素是原始数组中元素 + 1的结果;
 * 在创建一个新数组fount1, plus1数组中的元素每一个都与元素数组中的元素做对比，
 * 如果相等，那么fount数组对应元素 + 1;
 * 最后将fount中的元素统一 相加；
 *  原始数组      [1, 1, 3, 3, 5, 5, 7, 7]
 *  plus1:       [2, 2, 4, 4, 6, 6, 8, 8]
 *  fount:       [0, 0, 0, 0, 0, 0, 0, 0]
 *  count=        0 + 0 + 0 + 0 + 0 + 0 + 0 + 0*/

int method(int *arr, int length) {
    if (arr == nullptr || length == 0 || length == 1) {
        return -1;
    }
    int plus1[length];
    int fount[length];

    // 对元素数组相加操作，并且赋值给plus1数组
    for (int i = 0; i < length; i++) {
        plus1[i] = arr[i] + 1;
    }

    // 将plus1中的元素与原始数组相比较
    for (int i = 0; i < length; i++) {
        bool isFlag = false;
        for (int j = 0; j < length; j++) {
            if (plus1[i] == arr[j]) {
                isFlag = true;
            }
        }
        if(isFlag){
            fount[i] = 1;
        } else{
            fount[i] = 0;
        }
    }
    int count = 0;
    for (int i = 0; i < length; i++) {
        count += fount[i];
    }
    return count;
}
```

## 简便方法

[视频地址](https://www.bilibili.com/video/BV1od4y1i7tL?p=7&vd_source=50a5b75a7f57d35d5930d3e61d95378e)

# 第8天 查询LinkList的中位数

## 8.0 快慢指针的金典技巧

- 以一个大于两个元素的数组为例；

- 快指针走两步，慢指针走一步；
- 当快指针走到末尾，慢指针一定停留在数组中间；

> ​         [1, 4, 7, 2, 3, 5, 6, 4]
>
> slow               ^
>
> fast                             ^

## 8.1 查询一个数组的中位数

> [1, 2, 3, 4, 5]  数组的中位数为：5/2 == 2 也就是返回3<----> arr[5/2]
>
>  0, 1, 2, 3, 4
>
> 是偶数位数，就返回第二个中位数；
>
> [1, 2, 3, 4, 5, 6]  数组的中位数为：6/2 == 3 也就是返回4；arr[6/2]
>
>  0, 1, 2, 3, 4, 5

```c
#include <iostream>

int findMedian(const int *array, int length);

using namespace std;

int main(){
    int arr[] = {1, 2, 3, 4, 5, 6};
    printf("%d\n", findMedian(arr, sizeof (arr)/sizeof (arr[0])));
    exit(0);
}

int findMedian(const int *array, int length) {
    if(array == nullptr || length <= 0)
        return -1;
    return array[length/2];
}
```

## 8.2 查找链表的中位数

```c
#include <stdlib.h>
#include <stdio.h>



// 创建一个链表
typedef struct LinkList{
    int data;
    struct LinkList *next;
}LinkList;

// 链表的初始化
LinkList *initLinkList(){
    // 开辟一块空间
    LinkList *head = NULL;
    head = malloc(sizeof(LinkList));
    if(head == NULL) return NULL;
    head->next = NULL;
    return head;
}

// 链表的尾部插入数据
void insertData(LinkList *head, const int data){
    if(head == NULL ){
        exit(-1);
    }
    LinkList *newNode = NULL;
    newNode = malloc(sizeof(LinkList));
    if(NULL == newNode) exit(-1);

    newNode->data = data;
    newNode->next = NULL;

    LinkList *curr = head;
    while (curr->next != NULL)
        curr = curr->next;
    curr->next = newNode;
}

// 遍历输出链表
void selectLinkList(LinkList *head){
    if(head == NULL ){
        exit(-1);
    }
    LinkList* curr = head->next; // 从第一个节点开始遍历
    while (curr != NULL) {
        printf("%d\n", curr->data);
        curr = curr->next;
    }
}

// 返回链表最中间的数据
int selectMiddle(LinkList *head){
    if(head == NULL ){
        exit(-1);
    }
    LinkList *slow = head;
    LinkList *fast = head;
    while (fast != NULL && fast->next != NULL){
        slow = slow->next;
        fast = fast->next->next;
    }
    printf("%d\n", slow->data);
    return 0;
}


int main(){
    LinkList *head = initLinkList();
    for(int i = 1; i <= 7; i++){
        insertData(head, i);
    }
    // 查询中位数
    selectMiddle(head);
    
    // 遍历输出链表的数据
    selectLinkList(head);
    return 0;
}
```

# 第9天 删除#

> 例题1：S = "ab#c"; T = "ad#c";
>
> 删除#，以及#前面的一个字符；
>
> S = "ac"; T = "ac";    所以S == T;  那么就返回ture;
>
> 
>
> 例题2：S = "ab##"; T = "c#d#";
>
> 删除#，以及#前面的一个字符；
>
> S = ""; T = "";    所以S == T;  那么就返回ture;
>
> 
>
> 例题3：S = "a##c"; T = "#a#c";
>
> 删除#，以及#前面的一个字符；
>
> S = "c"; T = "c";    所以S == T;  那么就返回ture;
>
> 
>
> 例题4：S = "a#c"; T = "b";
>
> 删除#，以及#前面的一个字符；
>
> S = "c"; T = "b";    所以S != T;  那么就返回false;

## 9.1 求取字符串的长度

```c
# 给定已知的字符串
const char *str = "abcde";

int length = 0;
// strlen只会算 “” 内部的有多少个字符，不会多计算\0这个字符
length = strlen(str);    // 计算的结果为 5


// 但是我们在实际存储已知的字符串时，需要额为多加一个字符的位置 \0
const char *s = "abcw";   // 字符串的长度为4；

char store[strlen(s) + 1]; // + 1的操作就是为 \0站住一个位置
```



## 9.2 比较两个字符串

```c
strcmp(const char *str, const char *dest);

// 两个字符串相等 返回 0；
// 两个字符串不相等 返回 -1；
```



## 9.3 题目初始解

```c
#include <stdio.h>
#include <stdbool.h>
#include <string.h>

bool backSpaceCompare(char *S, char *T);

int main() {

    // 创建两个字符串
    char *S = "a#c";
    char *T = "c";
    printf("%d\n", backSpaceCompare(S, T));
    return 0;
}

bool backSpaceCompare(char *S, char *T){
    if(S == NULL || T == NULL){
        return false;
    }
    // 求取字符串S的长度
    int length = strlen(S);

    // 用一个新的阵列保存数据
    char result_S[length + 1];
    {
        int j = 0;
        for(int i = 0; i < length; i++){
            if(S[i] != '#'){
                result_S[j] = S[i];
                j++;
            }else{
                // 如果不等于 那就将j--.将字符覆盖
                if(j > 0){
                    j--;
                }
            }
        }
        result_S[j] = '\0';
    }

    // 求取字符串T的长度
    int length_T = strlen(T);
    char result_T[length_T + 1];
    {
        int j = 0;
        for(int i = 0; i < length_T; i++){
            if(T[i] != '#'){
                result_T[j] = T[i];
                j++;
            }else{
                if(j > 0){
                    j--;
                }
            }
        }
        result_T[j] = '\0';
    }
    return strcmp(result_S, result_T) == 0;
};
```



## 9.4 函式优化

```c
#include <stdio.h>
#include <stdbool.h>
#include <string.h>

bool backSpaceCompare(char *S, char *T);
void process(char *result, const char *str);

int main() {

    // 创建两个字符串
    char *S = "a#c#";
    //char *S = "a#c";
    char *T = "c";
    printf("%d\n", backSpaceCompare(S, T));
    return 0;
}

bool backSpaceCompare(char *S, char *T){
    if(S == NULL || T == NULL){
        return false;
    }
    // 求取字符串S的长度
    int length = strlen(S);

    // 用一个新的阵列保存数据
    char result_S[length + 1];
    process(result_S, S);

    // 求取字符串T的长度
    int length_T = strlen(T);
    char result_T[length_T + 1];
    process(result_T, T);
    return strcmp(result_S, result_T) == 0;
};

/*
 * 参数一：处理后的结果；
 * 参数二：原始字符串*/
void process(char *result, const char *str){
    int length = strlen(str);
    int j = 0;
    for(int i = 0; i < length; i++){
        if(str[i] != '#'){
            result[j] = str[i];
            j++;
        }else{
            // 如果不等于 那就将j--.将字符覆盖
            if(j > 0){
                j--;
            }
        }
    }
    result[j] = '\0';
}
```



## 9.5 函式继续优化

- 申请内存之后一定要记得释放

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>

bool backSpaceCompare(char *S, char *T);
char *process(const char *str);

int main() {

    // 创建两个字符串
    //char *S = "a#c#";
    char *S = "a#c";
    char *T = "c";
    printf("%d\n", backSpaceCompare(S, T));
    return 0;
}

bool backSpaceCompare(char *S, char *T){
    if(S == NULL || T == NULL){
        return false;
    }
    char *result_S = process(S);
    char *result_T = process(T);
    bool isEqual = (strcmp(result_S, result_T) == 0);
    free(result_S);
    free(result_T);
    return  isEqual;
};

/*
 * 参数一：处理后的结果；
 * 参数二：原始字符串*/
char *process(const char *str){
    int length = strlen(str);
    int j = 0;
    char *result = malloc(sizeof(char) * (length + 1));
    for(int i = 0; i < length; i++){
        if(str[i] != '#'){
            result[j] = str[i];
            j++;
        }else{
            // 如果不等于 那就将j--.将字符覆盖
            if(j > 0){
                j--;
            }
        }
    }
    result[j] = '\0';
    return result;
}
```



# 第10 天 栈的实现

队列是先进先出(FIFO, First In First Out)

栈是先进后出(FILO, First In Last Out)

## 10.1 基于定长数组的栈实现

```c
# 自定义样式
typedef struct{
    int data[100];
    int size;
}Stack
    
// 销毁只是销毁自定义样式
void destroyStack(Stack *stack){
    free(stack);
}

// 新增数据时，不需要额外加内存；
// 原因在于，自定义样式中已经申请了内存数组；
void push(Stack *stack, int x){
    stack->data[stack->size] = x;
    stack->size++;
}
```



```c
#include <stdio.h>
#include <stdlib.h>


// 自定义一个样式；
typedef struct{
    int data[100];
    int size;
}Stack;

Stack *initStack();
void push(Stack *stack, int x);
void printStack(Stack *stack);
int topData(Stack *stack);
void pop(Stack *stack);
void destroyStack(Stack *stack);

int main(){

    Stack *stack = initStack();

    // 入栈
    for(int i = 0; i < 10; i++){
        push(stack, i * 10);
    }

    // 打印输出栈
    // printStack(stack);

    // 弹出栈顶数据
    pop(stack);

    // 查看栈顶数组
    printf("%d\n", topData(stack));
    destroyStack(stack);
    exit(0);
}

Stack *initStack(){
    Stack *stack = malloc(sizeof (Stack));
    if(stack == NULL){
        return NULL;
    }
    stack->size = 0;
    return stack;
}

void push(Stack *stack, int x){
    stack->data[stack->size] = x;
    stack->size++;
}

void pop(Stack *stack){
    stack->size--;
}

int topData(Stack *stack){

    // c语言是从 0 开始计数的
    return stack->data[stack->size - 1];
}

void printStack(Stack *stack){
    for(int i = 0; i < stack->size; i++){
        printf("%d ",stack->data[i]);
    }
    printf("\n");
}

// 销毁栈
void destroyStack(Stack *stack){
    // 在销毁栈
    free(stack);
}
```

## 10.2 基于指针的栈实现

```c
# 自定义样式
typedef struct{
    int *data;
    int size;
}Stack
    
// 销毁栈
void destroyStack(Stack *stack){
    // 一定要记得释放,并且顺序不能反(先销毁自定义样式中的指针，在销毁自定义样式本身)
    free(stack->data);

    // 在销毁栈
    free(stack);
}

// 一定要给自定义的样式中存放数据的指针分配内存；
void push(Stack *stack, int x){
    // 加入数据的时候，一定要先扩大内存
    stack->data = realloc(stack->data, (sizeof (int) * (stack->size + 1)));

    // 存入数据
    stack->data[stack->size] = x;

    // 栈的元素个数加一
    stack->size++;
}
```





```c
#include <stdio.h>
#include <stdlib.h>


// 自定义一个样式；
typedef struct{
    int *data;
    int size;
}Stack;

Stack *initStack();
void push(Stack *stack, int x);
void printStack(Stack *stack);
int topData(Stack *stack);
void pop(Stack *stack);
void destroyStack(Stack *stack);

int main(){

    Stack *stack = initStack();

    // 入栈
    for(int i = 0; i < 15; i++){
        push(stack, i * 10);
    }

    // 打印输出栈
    printStack(stack);

    printf("***************************\n");

    // 弹出栈顶数据
    pop(stack);

    // 查看栈顶数组
    printf("%d\n", topData(stack));
    destroyStack(stack);
    exit(0);
}

Stack *initStack(){
    Stack *stack = malloc(sizeof (Stack));
    if(stack == NULL){
        return NULL;
    }
    // 初始化栈数据的指向
    stack->data = NULL;

    // 初始化栈的元素个数
    stack->size = 0;
    return stack;
}

void push(Stack *stack, int x){
    // 加入数据的时候，一定要先扩大内存
    stack->data = realloc(stack->data, (sizeof (int) * (stack->size + 1)));

    // 存入数据
    stack->data[stack->size] = x;

    // 栈的元素个数加一
    stack->size++;
}

void pop(Stack *stack){
    stack->size--;
}

int topData(Stack *stack){

    // c语言是从 0 开始计数的
    return stack->data[stack->size - 1];
}

void printStack(Stack *stack){
    for(int i = 0; i < stack->size; i++){
        printf("%d ",stack->data[i]);
    }
    printf("\n");
}

// 销毁栈
void destroyStack(Stack *stack){
    // 一定要记得释放,并且顺序不能反(先销毁自定义样式中的指针，在销毁自定义样式本身)
    free(stack->data);

    // 在销毁栈
    free(stack);
}
```



# 第11天 给定一棵二叉树，找出树中的最长路径



# 第12天 开心消消乐

> 给定一个数组 [2, 4, 1, 3, 8, 7]
>
> 首先找出最大的两个元素，让其中大得元素减去小的元素；拿出元素的位置置位为0；
>
> [2, 4, 1, 3, 0, 0]  将差插入0元素的位置；
>
> 所以 [2,  4，1, 3, 1，0]
>
> 继续得  4 -3
>
> [2, 0, 1, 0, 1, 0] 将差插入0元素的位置；
>
> 所以[2, 1, 1, 0, 1, 0] 
>
> 继续得
>
> [0, 0, 1, 0, 1, 0] 将差插入0元素的位置；
>
> 所以[1, 0, 1, 0, 1, 0] 
>
> [1]

源码分析；

```c
#include <stdio.h>


void insert(int *array, int length, int data){
    for(int i = 0; i < length; ++i){
        if(array[i] == 0){
            array[i] = data;
            return;
        }
    }
}

#if 0
// 找出数组中的最大一个值，将最大值返回，并且将该最大值所在的位置填充为零
int searchMax(int *array, int length){
    // 假定第一个数就是最大值
    int max = array[0];

    // 更新最大值
    for(int i = 1; i < length; ++i){
        if(array[i] > max){
            max = array[i];
        }
    }

    // 将最大值所在的位置置位为零；
    for(int i = 0; i < length; ++i){
        if(array[i] == max){
            array[i] = 0;
        }
    }
    //返回最大值
    return max;
}
#endif

int searchMax(int *array, int length){
    int index = 0;
    for(int i = 1; i < length; i++){
        if(array[i] > array[index]){
            // 更新索引
            index = i;
        }
    }
    int max = array[index];
    array[index] = 0;
    return max;
}


int lastStoneWeight(int *array, int length){
    while(1){
        // 找出最大值
        int x = searchMax(array, length);

        // 找出次大值
        int y = searchMax(array, length);

        if(y == 0){
            return x;
        }

        if(x != y){
            // 将差插入到数组中的零位置
            insert(array, length, (x - y));
        }
    }
    return 0;
}

int main(void){
    // 定义一个数组
    int array[] = {2, 7, 4, 1, 8, 1};
    int result = lastStoneWeight(array, sizeof (array)/ sizeof(array[0]));
    printf("剩余结果为：%d\n", result);
    return 0;
}
```



