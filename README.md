## Main differences
### Алгоритм 1: разделение по строкам

Матрица A разбивается на куски по строкам и каждый кусок передаётся процессу с помощью MPI.Scatter
Матрица B передаётся полностью с помощью MPI_Bcast
Каждый процесс вычисляет свой кусок матрицы C
Полученные куски матрицы C собираются с помощью MPI_Gather

### Алгоритм 2: разделение по столбцам

Матрица B разбивается на куски по столбцам и каждый кусок передаётся процессу с помощью MPI.Scatter
Матрица A передаётся полностью с помощью MPI_Bcast
Каждый процесс вычисляет свой кусок матрицы C
Полученные куски матрицы C суммируются с помощью MPI_Reduce
### Алгоритм 3: разделение на блоки

Матрица A разбивается на блоки и каждый блок передаётся соответствующему процессу с помощью MPI_Send/MPI_Recv
Матрица B передаётся полностью с помощью MPI_Bcast
Каждый процесс вычисляет свой кусок матрицы C
Полученные куски матрицы C суммируются с помощью MPI_Reduce

## Performance results:
### Row result:

|threads|24          |240       |1200    |2400    |
|-------|------------|----------|--------|--------|
|1      |0.000122961s|0.125914s |15.9193s|128.896s|
|2      |0.000095831s|0.0632039s|8.30663s|68.3042s|
|4      |0.00006398s |0.0347621s|4.76348s|39.1462s|
|6      |0.00004895s |0.0306727s|3.90481s|32.4664s|
|12     |0.0300235s  |0.0244012s|3.28949s|25.4955s|

![image](https://user-images.githubusercontent.com/62809413/227742539-a370e197-9478-4913-b02a-1d9793bd238c.png)

### Column result:
|threads|24          |240       |1200    |2400    |
|-------|------------|----------|--------|--------|
|1      |0.000146506s|0.13071s  |16.4175s|131.133s|
|2      |0.000076155s|0.0662777s|8.66546s|69.2095s|
|4      |0.000058961s|0.0375937s|5.03359s|39.929s |
|6      |0.000078959s|0.0429893s|4.13577s|32.3348s|
|12     |0.00006913s |0.026251s |3.50785s|24.7307s|

![image](https://user-images.githubusercontent.com/62809413/227742834-a4e90cb6-2957-4310-bd43-a39913fd1bdf.png)

### Block result:
|threads|24          |240       |1200    |2400    |
|-------|------------|----------|--------|--------|
|1      |0.000101521s|0.0991533s|12.3665s|101.931s|
|2      |0.000060394s|0.0497441s|6.5417s |52.7878s|
|4      |0.000052268s|0.0398471s|3.88501s|29.5543s|
|6      |0.000195087s|0.0283722s|3.13157s|24.9304s|
|12     |0.000188614s|0.0199715s|2.48687s|19.0995s|

![image](https://user-images.githubusercontent.com/62809413/227742902-2b844cf4-bd2e-42c2-80b2-07d9dd6bccf1.png)

