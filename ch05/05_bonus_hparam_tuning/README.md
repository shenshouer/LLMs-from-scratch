# 为预训练优化超参数

[hparam_search.py](hparam_search.py)脚本基于[附录D：为训练循环扩展更多功能](../../appendix-D/01_main-chapter-code/appendix-D.ipynb)中添加的扩展训练功能，旨在通过网格搜索找到最佳超参数。

>[!NOTE]
这个脚本运行时间可能较长。您可能希望在顶部的HPARAM_GRID字典中减少要探索的超参数配置数量