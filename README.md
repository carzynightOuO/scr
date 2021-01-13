# 最短路徑 (Floyd-Warshall 演算法)介紹
Floyd-Warshall演算法（英語：Floyd-Warshall algorithm），中文亦稱弗洛伊德演算法或佛洛依德演算法[1]，是解決任意兩點間的最短路徑的一種演算法[2]，可以正確處理有向圖或負權（但不可存在負權迴路）的最短路徑問題，同時也被用於計算有向圖的遞移閉包[3]。
Floyd-Warshall演算法的時間複雜度為{\displaystyle O(N^{3})}O(N^{3})[4]，空間複雜度為{\displaystyle O(N^{2})}O(N^{2})。

# 程式碼
import numpy as np
import pandas as pd

inf = 99999999
e = np.zeros((10,10), dtype = np.int)

n, m = map(int, input().split(' '))

#initialize
for i in range(1, n+1):
	for j in range(1, n+1):
		if i==j:
			e[i][j]=0
		else:
			e[i][j]=inf

#read line
for i in range(1, m+1):
	t1, t2, t3 = map(int, input().split(' '))
	e[t1][t2]=t3

#Floyd-Warshall algorithm
for k in range(1, n+1):
	for i in range(1, n+1):
		for j in range(1, n+1):
			if e[i][j] > e[i][k]+e[k][j]:
				e[i][j] = e[i][k]+e[k][j]

 test data:
 4 8
 1 2 2
 1 3 6
 1 4 4
 2 3 3
 3 1 7
 3 4 1
 4 1 5
 4 3 12

output final consequences
for i in range(1, n+1):
    print(e[i][1:n+1])

 ---------------------
 # 最終結果
 [0 2 5 4]
 [9 0 3 4]
 [6 8 0 1]
 [ 5  7 10  0]

# 　 		1		2		3 		4
# 1		0		2		5 		4
# 2		9		0		3  		4
# 3		6		8		0		 1
# 4		5		7		10		0
