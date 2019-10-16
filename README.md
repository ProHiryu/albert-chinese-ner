# albert-chinese-ner

## 前言

这次的albert某种程度上可能比bert本身更具有意义，恰逢中文预训练模型出来，还是按照之前的数据来做一次NER方面的fine-tune，看看效果如何

PS: 移步传统[**bert ner**](https://github.com/ProHiryu/bert-chinese-ner)模型

## Resources

- [Bert](https://github.com/google-research/bert)
- [ALBert](https://github.com/albertlauncher/albert)
- [ALBert_zh](https://github.com/brightmart/albert_zh)

## Papers

- [ALBERT](https://arxiv.org/pdf/1909.11942.pdf)

## 配置

1. 下载albert中文模型，这里使用的是base
2. 将模型文件夹重命名为albert_base_zh，放入项目中
3. 运行
   ```bash
   python albert_ner.py --task_name ner --do_train true --do_eval true --data_dir data --vocab_file ./albert_config/vocab.txt --bert_config_file ./albert_base_zh/albert_config_base.json --max_seq_length 128 --train_batch_size 64 --learning_rate 2e-5 --num_train_epochs 3 --output_dir albert_base_ner_checkpoints
   ```
4.最好使用tensorflow > 1.13, 这里运行的是1.15，不支持tf2.0

## 结果

Base模型下训练3个epoch后：

```bash
INFO:tensorflow:  eval_f = 0.9280548
INFO:tensorflow:  eval_precision = 0.923054
INFO:tensorflow:  eval_recall = 0.9331808
INFO:tensorflow:  global_step = 2374
INFO:tensorflow:  loss = 13.210413
```

测试结果同样：

```
[CLS]
B-LOC
I-LOC
O
B-LOC
I-LOC
I-PER
O
O
O
O
O
O
O
O
O
[SEP]
[CLS]
```

## 总结

比起Bert本体，模型确实小了很多，效果却基本相当甚至领先bert，训练时间大幅缩小，NLP的“大舰巨炮”时代可能真的要过去了