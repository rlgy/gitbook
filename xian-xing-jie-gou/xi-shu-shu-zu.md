---
description: 压缩数组数据
---

# 稀疏数组

将一个规模为N\*M的数组压缩为一个N\*3的数组，这个数组就叫做稀疏数组。稀疏数组的第一行分别保存被压缩数组的行列以及有效数据的个数。

```text
#include <stdio.h>
#include <stdlib.h>

#define N 11
#define M 11
#define INVALID_NUMBER 0

int main() {
    // 原始数组
    int arr[N][M] = {0};
    // 指向稀疏数组的指针,指向根据稀疏数组获取到的原始数据的数组
    int **sparseArr, **originArr;
    // 有效数据的个数, 当前是第几个有效数据
    int sum = 0, count = 0;
    // 原始数组的行和列
    int n = N, m = M;

    // 原始数据数据填充
    arr[1][2] = 1;
    arr[2][3] = 2;
    // 打印原始数据
    printf("原始数组的数据:\n");
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            printf("%d\t", arr[i][j]);
        }
        printf("\n");
    }
    // 获取原始数据的有效数据个数
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            if (INVALID_NUMBER != arr[i][j]) {
                sum++;
            }
        }
    }
    printf("有效数据个数: %d\n", sum);
    // 创建压缩数组
    sparseArr = (int **) malloc(sizeof(int *) * (sum + 1));
    for (int i = 0; i < sum + 1; ++i) {
        sparseArr[i] = (int *) calloc(3, sizeof(int));
    }
    sparseArr[0][0] = n;
    sparseArr[0][1] = m;
    sparseArr[0][2] = sum;

    // 压缩原始数据为一个稀疏数组
    count = 1;
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            if (INVALID_NUMBER != arr[i][j]) {
                sparseArr[count][0] = i;
                sparseArr[count][1] = j;
                sparseArr[count][2] = arr[i][j];
                count++;
            }
        }
    }
    // 打印稀疏数组的数据
    printf("稀疏数组的数据:\n");
    for (int i = 0; i < sum + 1; ++i) {
        for (int j = 0; j < 3; ++j) {
            printf("%d\t", sparseArr[i][j]);
        }
        printf("\n");
    }

    // 根据稀疏数组获取原始数组的数据
    n = sparseArr[0][0];
    m = sparseArr[0][1];
    sum = sparseArr[0][2];
    // 初始化原始保存原始数据的数组
    originArr = (int **) malloc(sizeof(int *) * n);
    for (int i = 0; i < n; ++i) {
        originArr[i] = (int *) calloc(m, sizeof(int));
    }

    // 还原数据
    for (int i = 1; i < sum + 1; ++i) {
        originArr[sparseArr[i][0]][sparseArr[i][1]] = sparseArr[i][2];
    }
    // 打印还原后的数据
    printf("还原后的数据: \n");
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            printf("%d\t", originArr[i][j]);
        }
        printf("\n");
    }

    return 0;
}

```

运行结果：

```text
原始数组的数据:
0	0	0	0	0	0	0	0	0	0	0	
0	0	1	0	0	0	0	0	0	0	0	
0	0	0	2	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
有效数据个数: 2
稀疏数组的数据:
11	11	2	
1	  2	  1	
2	  3	  2
还原后的数据: 
0	0	0	0	0	0	0	0	0	0	0	
0	0	1	0	0	0	0	0	0	0	0	
0	0	0	2	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	
0	0	0	0	0	0	0	0	0	0	0	

```



