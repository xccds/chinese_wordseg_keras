基于深度学习的中文分词尝试

最近研究deeplearning和NLP比较多，其实就是在看Stanford的cs224d课程啦（http://cs224d.stanford.edu/syllabus.html）。抽空尝试了一下使用词向量和神经网络做中文分词。

使用的数据是参考资料中的中文分词资源，即Bakeoff中微软研究院的中文语料库，它的训练文本带有每个字的标注（BEMS），同时带有测试文本和测试脚本。此外使用了补充的语料库，即sogou新闻语料库，不带字标注，但可用来学习字向量。

使用的工具是python中的gensim库和keras库，gensim可用于学习词向量，keras是基于theano的深度学习库。在本例中只使用了普通的MLP方法。

整体工作的步骤如下：
- 步骤1：使用sogou的语料库建立初始的字向量，向量维度为100，迭代50次。
- 步骤2：读入有标注的训练语料库，处理成keras需要的数据格式。
- 步骤3：根据训练数据建模，使用左右各3个字做为上下文，7*100个神经元为输入层，隐藏层为100，输出层为4，神经网络结构为[700->100->4]，总共进行了约50次迭代。
- 步骤4：读入无标注的测试语料库，用训练得到的神经网络进行分词标注
- 步骤5：使用自动脚本检查最终的效果

最终测试脚本输出的summary如下。

=== SUMMARY:
=== TOTAL INSERTIONS:	2872
=== TOTAL DELETIONS:	2896
=== TOTAL SUBSTITUTIONS:	6444
=== TOTAL NCHANGE:	12212
=== TOTAL TRUE WORD COUNT:	106873
=== TOTAL TEST WORD COUNT:	106849
=== TOTAL TRUE WORDS RECALL:	0.913
=== TOTAL TEST WORDS PRECISION:	0.913
=== F MEASURE:	0.913
=== OOV Rate:	0.026
=== OOV Recall Rate:	0.673
=== IV Recall Rate:	0.919


后续折腾畅想：
- 本例中带标注的语料库相当大，可以直接在这个上面先训练字向量试试。
- 有空时还可以测试下jieba分词的效果评估。
- 用RNN等其它的方法试试效果。


参考资料:
[中文分词资源](http://www.52nlp.cn/%E4%B8%AD%E6%96%87%E5%88%86%E8%AF%8D%E5%85%A5%E9%97%A8%E4%B9%8B%E8%B5%84%E6%BA%90) 
[中文分词标注法](http://www.52nlp.cn/the-character-based-tagging-method-of-chinese-word-segmentation) 
[word2vec原理](http://suanfazu.com/t/word2vec-zhong-de-shu-xue-yuan-li-xiang-jie-duo-tu-wifixia-yue-du/178) 
[基于word2vec的中文分词](http://blog.csdn.net/itplus/article/details/17122431)
