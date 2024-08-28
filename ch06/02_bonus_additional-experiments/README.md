# 额外的分类微调实验


下表添加了实验,以回答有关各种设计选择的其他问题。第一行使用与主章相同的设置,并作为参考。

例如,

- 比较行1和2的答案是:"当我们训练最后一个或第一个Token时,性能差异是什么?";
- 比较行1和3的答案是:"当我们训练最后一个层而不是最后一个块时,性能差异是什么?";
- 等等。

&nbsp;

|     | 模型               | 权重       | 可训练的token位置 | 可训练的层      | 上下文长度                                             | 训练准确率 | 验证准确率 | 测试准确率 | 训练时间 | CPU/GPU |
| --- | ------------------ | ---------- | ----------------- | --------------- | ------------------------------------------------------ | ---------- | ---------- | ---------- | -------- | ------- |
| 1   | gpt2-small (124M)  | pretrained | last              | last_block      | longest train ex. (120)                                | 96.63%     | 99.33%     | 95.00%     | 0.28 min | A100    |
| 2   | gpt2-small (124M)  | pretrained | first             | last_block      | longest train ex. (120)                                | 78.46%     | 80.54%     | 75.00%     | 0.28 min | A100    |
| 3   | gpt2-small (124M)  | pretrained | last              | last_layer      | longest train ex. (120)                                | 78.65%     | 79.87%     | 72.00%     | 0.25 min | A100    |
| 4   | gpt2-small (124M)  | pretrained | last              | last_two_blocks | longest train ex. (120)                                | 98.85%     | 98.66%     | 98.33%     | 0.33 min | A100    |
| 5   | gpt2-small (124M)  | pretrained | last              | all             | longest train ex. (120)                                | 99.62%     | 96.64%     | 96.67%     | 0.69 min | A100    |
| 6   | gpt2-medium (355M) | pretrained | last              | last_block      | longest train ex. (120)                                | 87.50%     | 91.28%     | 84.67%     | 0.75 min | A100    |
| 7   | gpt2-large (774M)  | pretrained | last              | last_block      | longest train ex. (120)                                | 99.52%     | 98.66%     | 96.67%     | 1.50 min | A100    |
| 8   | gpt2-xl (1558M)    | pretrained | last              | last_block      | longest train ex. (120)                                | 99.81%     | 99.33%     | 98.33%     | 2.83 min | A100    |
| 9   | gpt2-small (124M)  | random     | last              | all             | longest train ex. (120)                                | 100.00%    | 96.64%     | 93.67%     | 0.69 min | A100    |
| 10  | gpt2-small (124M)  | pretrained | last              | LoRA            | longest train ex. (120)                                | 100.00%    | 97.32%     | 96.67%     | 0.75 min | A100    |
| 11  | gpt2-small (124M)  | pretrained | last              | last_block      | context length (1024)                                  | 83.08%     | 87.92%     | 78.33%     | 2.46 min | A100    |
| 12  | gpt2-small (124M)  | pretrained | last              | last_block      | variable: no padding (batch size 1)                    | 100.00%    | 98.66%     | 98.00%     | 1.75 min | A100    |
| 13  | gpt2-small (124M)  | pretrained | last              | last_block      | variable: no padding (batch size 8)                    | 99.33%     | 98.66%     | 98.33%     | 1.70 min | A100    |
| 14  | gpt2-small (124M)  | pretrained | last              | last_block      | longest train ex. (120); but no causal mask            | 99.23%     | 98.66%     | 95.33%     | 0.29 min | A100    |
| 15  | gpt2-small (124M)  | pretrained | last              | last_block      | longest train ex. (120) and `ignore_index` for padding | 96.63%     | 99.33%     | 95.00%     | 0.28 min | A100    |

&nbsp;

### 使用方法

您可以使用以下代码来复现实验：

- Row 1: `python additional-experiments.py`
- Row 2: `python additional-experiments.py --trainable_token_pos first`
- Row 3: `python additional-experiments.py --trainable_layers last_layer`
- Row 4: `python additional-experiments.py --trainable_layers last_two_blocks`
- Row 5: `python additional-experiments.py --trainable_layers all`
- Row 6: `python additional-experiments.py --model_size "gpt2-medium (355M)"`
- Row 7: `python additional-experiments.py --model_size "gpt2-large (774M)"`
- Row 8: `python additional-experiments.py --model_size "gpt2-xl (1558M)"`
- Row 9: `python additional-experiments.py --weights random --trainable_layers all`
- Row 10: `python additional-experiments.py --trainable_layers lora --lora_rank 16 --lora_alpha 16`
- Row 11: `python additional-experiments.py --context_length "model_context_length"`
- Row 12: `python additional-experiments.py --no_padding --batch_size 1`
- Row 13: `python additional-experiments.py --no_padding --batch_size 1 --accumulation_steps 8`
- Row 14: `python additional-experiments.py --disable_causal_mask`
- Row 15: `python additional-experiments.py --ignore_index 50256`

我特意保持了大语言模型和数据集的规模较小,这样即使您没有GPU,也可以在普通笔记本电脑上运行训练,比如在MacBook Air M3上大约15分钟就能完成（对于默认设置）。

&nbsp;

### 解释

1. **训练最后vs第一个输出token位置（第1行vs第2行）**：训练最后一个输出token位置比第一个获得了显著更好的性能。由于因果自注意力掩码的存在,这种改进是可以预期的。
2. **训练最后Transformer块与最后层（第1行vs第3行）**：训练整个最后Transformer块比仅训练最后层的结果显著更好。
3. **训练最后与最后两个Transformer块（第1行vs.第4行）**：训练最后两个Transformer块而不是仅训练最后块的结果明显提高了3.33%的准确率。
4. **训练最后Transformer块与所有层（第1行vs.第5行）**：训练所有层仅比训练最后Transformer块略微提高了~2%的准确率，但训练时间却几乎长3倍。此外，它比仅训练最后两个Transformer块的性能稍差。
5. **使用更大的预训练模型（第1行vs.第6行，第1行vs.第7行和第8行）**：使用3倍大的预训练模型会导致更差的结果。然而，使用5倍大的模型比初始模型提高了性能，这符合预期。同样，12倍大的模型进一步提高了预测性能。（也许这个中型模型没有很好地预训练，或者这种特定的微调配置在这个模型上效果不佳。）
6. **使用具有随机权重的模型与预训练权重（第1行和第5行vs.第9行）**：使用具有随机权重的模型仅比使用预训练权重稍差（分别为3%和1.3%）。
7. **使用LoRA（低秩适应）与训练所有层（第10行vs.第5行）**：保持模型冻结并添加可训练的LoRA层（有关详细信息，请参见[附录E](../../appendix-E/01_main-chapter-code/appendix-E.ipynb)）是一种可行的替代方案，即使训练所有模型参数，性能也提高了1%点。通过使用LoRA，它甚至更节省内存，因为更少的参数需要更新。
8. **将输入填充到完整上下文长度 vs. 最长训练样例（第1行 vs. 第11行）**：将输入填充到支持的完整上下文长度会导致性能显著下降。
9. **使用填充 vs 不使用填充（第1行 vs. 第12行和第13行）**：`--no_padding`选项禁用了数据集中的填充,这要求以批量大小为1来训练模型,因为输入长度不一。这导致了更好的测试准确率,但训练时间更长。在第12行中,我们额外启用了8步的梯度累积,以达到与其他实验相同的批量大小,这有助于减少过拟合并略微提高测试集准确率。
10. **禁用因果注意力掩码（第1行 vs. 第14行）**：禁用多头注意力模块中使用的因果注意力掩码。这意味着所有token都可以关注其他所有token。与使用因果掩码的GPT模型相比,模型准确率略有提高。
11. **在损失和反向传播中忽略填充索引（第1行 vs. 第15行）**：设置`--ignore_index 50256`在PyTorch的`cross_entropy`损失函数中排除了`|endoftext|`填充token。在这个例子中,它没有任何效果,因为我们替换了输出层,使得token ID只能是0或1（用于二元分类）。然而,这个设置在第7章的指令微调模型时很有用。
