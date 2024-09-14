| 这个作业属于哪个课程 | https://edu.cnblogs.com/campus/gdgy/CSGrade22-12                |
| ---------- | --------------------------------------------------------------- |
| 这个作业要求在哪里  | https://edu.cnblogs.com/campus/gdgy/CSGrade22-12/homework/13220 |
| 这个作业的目标    | 学会论文查重算法，学会使用git等操作                                             |
|github 地址|https://github.com/nurimanguli/3222004935/tree/main|

| PSP2.1                                | Personal Software Process Stages | 预估耗时（分钟） | 实际耗时（分钟） |
| ------------------------------------- | -------------------------------- | -------- | -------- |
| Planning                              | 计划                               | 100     | 180      |
| Estimate                              | 估计这个任务需要多少时间                     | 20     | 30     |
| Development                           | 开发                               | 360      | 360      |
| Analysis                              | 需求分析（包括学习新技术）                    | 100      | 120      |
| Design Spec                           | 生成设计文档                           | 20      | 20       |
| Design Review                         | 设计审核                             | 10       |10       |
| Coding Standard                       | 代码规范（为目前的开发制定合适的规范）              | 5      | 30       |
| Design                                | 具体设计                             | 20      |30      |
| Coding                                | 具体编码                             | 125      | 180     |
| Code Review                           | 代码审核                             |20      | 15       |
| Test                                  | 测试（自我测试，修改代码，提交修改）               |60      | 120      |
| Reporting                             | 报告                               | 40      | 45      |
| Test Report                           | 测试报告                             | 20     |30       |
| Size Measurement                      | 计算工作量                            | 10      | 20       |
| Postmortem & Process Improvement Plan | 事后总结，并提出过程改进计划                   | 10       | 40       |
| 合计                                    | 1475                             | 620    |  1310        |
程序结构：![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914192343374-1382299561.png)
如上图所示：

TooException：控制用以SimHash计算的文字不少于300字；

TxtException：控制读取的文件仅为.txt型的文档；

MainText：主函数，用以开发时的逐步测试和最后的运行；

HammingUtils：Hamming算法的集合，参数：两端文字的hash值组； 返回：海明距离；

SimHashUtils：SimHash算法的集合，参数：要比较的文字； 返回：各个特征向量（这里为划分好的词）的hash值，hash值为二进制数01组成的n-bit签名；

TxtIOUtils：重写读取和读入的方法，使之符合要求；
三、各阶段分析与结果：
第一次提交：
内容：约束函数，simhash计算函数，主函数（测试函数）；
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914192641075-2000650572.png)
第二次提交：
内容：Hamming计算函数；

运行结果：
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914192851490-1905318807.png)
第三次提交：
内容：

-->文档相关的操作，包括将文档加入项目中、文档的读取和读入等，修改了主函数还有其它函数，调整到能完全进行文件操作；

-->根据运行类编译测试类；

运行结果:
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914192920666-1742880120.png)
文档结果显示：
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914192953025-357567533.png)
四、测试分析：
Exception：
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914193029384-469788779.png)
MainText：
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914193056417-1047435620.png)
Utils：
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914193121363-281878788.png)
五、 性能分析：
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914193414563-1432282195.png)
![](https://img2024.cnblogs.com/blog/3516401/202409/3516401-20240914204757463-329226511.png)

代码：
import difflib  # 导入查重包
import argparse  # 导入命令行包
import os.path

# 命令行输入文件路径
parser = argparse.ArgumentParser(description='命令行传入文件路径')
parser.add_argument('path1', type=str, help='原文文件')
parser.add_argument('path2', type=str, help='抄袭版的论文文件')
parser.add_argument('path3', type=str, help='答案文件')
paths = parser.parse_args()

# 读取path1和path2的文件
if os.path.isfile(paths.path1):
    with open(paths.path1, 'r', encoding='utf-8') as file1:
        a = file1.read()
else:
    print('path1的路径错误或不存在')
if os.path.isfile(paths.path2):
    with open(paths.path2, 'r', encoding='utf-8') as file2:
        b = file2.read()
else:
    print('path2的路径错误或不存在')

if os.path.isfile(paths.path1) & os.path.isfile(paths.path2):
    # 创建一个SequenceMatcher对象
    sm = difflib.SequenceMatcher(None, a, b)

    # 计算并打印两篇文章的相似度
    with open(paths.path3, 'w', encoding='utf-8') as fp:
        similarity = sm.ratio()
        print('差异报告：', file=fp)
        print(f'相似度：{similarity:.2f}', file=fp)
        fp.close()
