#NLP问答与推理，查阅的资料
##路径
***数据清洗（去掉停用词）--》中文分词--》机器翻译（encoder->attention->decoder)***
###引入
1、目前深度学习方法在对自然语言处理方面的基本方向是通过对文档上下文进行学习训练，对于中文文档，还需要先进行中文分词处理，然后将文档中的词语、句子分别用连续实值向量进行表示，形成的向量称为嵌入向量，这样做是为了方便处理文本语义特征，将词语、句子用向量表示，在处理文本语义特征时，对词向量、句向量直接进行向量上的计算即可表征它们之间的文本语义关系。
2、第一步就是将自然语言转化为机器可以理解的语言，于是想到将它进行符号数学化，为了能表示多维特征，增强其泛化能力，想到用向量对其进行表示，因此也就引出了对词向量、句向量的研究。
3、Seqence-to-Sequence 模型广泛应用于机器翻译、语音识别、视频图片处理、文本摘要等多个领域。现在最新的一些基于深度学习研究文本摘要生成方法的也都是基于这个模型进行的。基于Seqence-to-Sequence 模型的文本摘要需要解决的问题是从原文本到摘要文本的映射问题。
4、考虑到句子中的某些特定词或特定词性的词更具有影响句子中心意思的作用，引入了广泛应用于机器翻译中的注意力机制（attention mechanism）对句子的不同部分赋予不同的偏重，即权重。Rush 等在这个基础上提出基于注意力模型的生成式文本摘要
5、（GAN）Liu 将广泛应用于图像领域的生成对抗网络（GAN, generative adversarial networks）借用于文本摘要领域取得了显著成效，提出了一种生成式文本摘要的生成对抗过程，在这个过程中，同时训练一个生成模型 G 和一个判别型D。生成器通过文本的输入来预测生成摘要，判别器则试图将机器生成的摘要与真实摘要进行区分。在这个博弈过程中，双方不断提高性能，最后利用训练得到的生成器生成与真实摘要基本吻合的机器摘要。
###生成式摘要
1、Seq2Seq 来完成生成式摘要存在如下问题：（1）未登录词问题（OOV），（2）生成重复。现在被广泛应用于生成式摘要的框架由 See 等人[13]在 ACL17 中提出，在基于注意力机制的 Seq2Seq 基础上增加了 Copy 和 Coverage 机制，有效的缓解了上述问题。
###抽取生成式摘要
抽取式、生成式摘要各有优点，为了结合两者的优点，一些方法也同时使用抽取结合生成的方法来完成摘要任务。
--
从直觉上来讲，摘要任务可以大致分为两步，首先选择重要内容，其次进行内容改写。在 EMNLP18 中，Gehrmann 等人[2]基于这种想法，提出了“Bottom Up”方式的摘要， 首先使用“content selector”选择关键信息，其次使用 pointer-generator 网络生成摘要。

---
##小点
理解停用词表  ：https://blog.csdn.net/qq_41853758/article/details/82924765
        抽取式摘要中需要通过词频来判断词得知重要性。除去停用词以外，文中出现频率越高的单词，其重要性也就越高。
--
由于语言和应用的多样性，我们需要先对原始的文本进行分词、去除停用词等操作，得到每一篇文档的特征列表。然后才能进行导入模型的训练。

---
##文本摘要
###理解文献
**推荐阅读**文本摘要系统性学习： https://zhuanlan.zhihu.com/p/67078700
自动文本摘要理解1：https://blog.csdn.net/zz133110/article/details/75402953
 ###实操
1、简单摘要方法：抽取每一次对话的第一句、中间句、最后一句
2、基于传统统计方法TextRank算法： http://blog.itpub.net/31562039/viewspace-2286669/

---
##机器翻译
paddlepaddle源代码：https://www.paddlepaddle.org.cn/documentation/docs/zh/user_guides/nlp_case/machine_translation/README.cn.html
--
pandas官网提供得NMT代码：
https://www.pypandas.cn/deep/basics/machine_translation.html

---
#词向量
pandas官网提供的各种模型：
https://www.pypandas.cn/deep/basics/word2vec.html

---
##库的使用
###jieba库
1、官方教程： https://github.com/fxsjy/jieba
2、jieba库简明教程 ：https://www.jianshu.com/p/883c2171cdb5
###Gensim库
1、*对原始文本进行分词/去除停用词：*
由于语言和应用的多样性，我们需要先对原始的文本进行分词、去除停用词等操作，得到每一篇文档的特征列表。然后才能进行导入模型的训练。
2、*将原始文本表达转化为稀疏向量的表达方式（词向量？）：*
可以调用Gensim提供的API建立语料特征（此处即是word）的索引字典，并将文本特征的原始表达转化成词袋模型对应的稀疏向量的表达。
--
1、官网教程： https://radimrehurek.com/gensim/auto_examples/index.html
2、使用Gensim模块训练词向量： https://zhuanlan.zhihu.com/p/40016964
3、Gensim分词/词向量/字典DEMO: https://www.cnblogs.com/chenyibai/p/10735417.html
###pandas库
1、官网教程：https://www.pypandas.cn/docs/
