# 为预训练优化超参数

[hparam_search.py](hparam_search.py)脚本基于[附录D：为训练循环扩展更多功能](../../appendix-D/01_main-chapter-code/appendix-D.ipynb)中添加的扩展训练功能，旨在通过网格搜索找到最佳超参数。

>[!NOTE]
This script will take a long time to run. You may want to reduce the number of hyperparameter configurations explored in the `HPARAM_GRID` dictionary at the top.