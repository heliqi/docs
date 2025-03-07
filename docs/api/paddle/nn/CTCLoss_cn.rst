.. _cn_api_paddle_nn_CTCLoss:

CTCLoss
-------------------------------

.. py:class:: paddle.nn.CTCLoss(blank=0, reduction='mean')

该接口用于计算 CTC loss。该接口的底层调用了第三方 baidu-research::warp-ctc 的实现。
也可以叫做 softmax with CTC，因为 Warp-CTC 库中插入了 softmax 激活函数来对输入的值进行归一化。

参数
:::::::::
    - **blank** (int，可选): - 空格标记的 ID 值，其取值范围为 [0，num_classes+1)。数据类型支持 int32。默认值为 0。
    - **reduction** (string，可选): - 指定应用于输出结果的计算方式，可选值有：``'none'``, ``'mean'``, ``'sum'``。设置为 ``'mean'`` 时，对 loss 值除以 label_lengths，并返回所得商的均值；设置为 ``'sum'`` 时，返回 loss 值的总和；设置为 ``'none'`` 时，则直接返回输出的 loss 值。默认值为 ``'mean'``。

形状
:::::::::
    - **logits** (Tensor): - 经过 padding 的概率序列，其 shape 必须是 [max_logit_length, batch_size, num_classes + 1]。其中 max_logit_length 是最长输入序列的长度。该输入不需要经过 softmax 操作，因为该 OP 的内部对 input 做了 softmax 操作。数据类型仅支持 float32。
    - **labels** (Tensor): - 经过 padding 的标签序列，其 shape 为 [batch_size, max_label_length]，其中 max_label_length 是最长的 label 序列的长度。数据类型支持 int32。
    - **input_lengths** (Tensor): - 表示输入 ``logits`` 数据中每个序列的长度，shape 为 [batch_size]。数据类型支持 int64。
    - **label_lengths** (Tensor): - 表示 label 中每个序列的长度，shape 为 [batch_size]。数据类型支持 int64。

返回
:::::::::
``Tensor``，输入 ``logits`` 和标签 ``labels`` 间的 `ctc loss`。如果 :attr:`reduction` 是 ``'none'``，则输出 loss 的维度为 [batch_size]。如果 :attr:`reduction` 是 ``'mean'`` 或 ``'sum'``，则输出 Loss 的维度为 [1]。数据类型与输入 ``logits`` 一致。

代码示例
:::::::::

COPY-FROM: paddle.nn.CTCLoss
