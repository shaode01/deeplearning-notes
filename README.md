"# deeplearning-notes" 
# deeplearning-notes
hyperparameter tuning
how to set up your data
深度学习要调很多参数，没办法一次准确的猜测所有的参数，所以在实际应用中，这是一个高度迭代（very iterative）的过程，通常你是先有个idea，然后建一个神经网络，然后跑一下看看效果，根据结果来调整参数。通常一个领域的intuition并不会迁移到另一个领域。最优解可能取决于你拥有的数据量、特征数目、电脑配置、用GPU还是CPU。所以决定你的进度有多快的一个因素是你能多快地完成一轮迭代。
1，合理地设置训练数据集、development数据集（hold-out cross validation set）和测试数据集的大小。
我们在训练数据集上训练，在dev数据集上验证哪个模型表现最好并挑选模型，最终的结果用测试数据集评判。
在以前通常划分为70%训练数据集，30%测试数据集，或者60%训练数据集，20%验证数据集（dev数据集），20%测试数据集。
但在现在有大量的数据的时候，dev数据集和test数据集可以比例更小，因为dev数据集和存在的目的是测试哪个模型更好，所以他们只要足够大就行。比如有100万个样本，1万个样本足够用来判断哪个模型更好了。同样的test数据集的目的是给你一个关于模型有多好的无偏的估计。所以最终这一百万的数据可能划分为98万测试数据集，1万dev数据集，1万test数据集。
另一个趋势是越来越多的人的训练数据集和测试数据集的分布不同。但吴恩达建议保证dev数据集和测试数据集的分布一致。
由于deep learning对训练数据的需求是如此之大，很多时候我们会从各种来源搜集数据，因此即使训练数据集来自于不同的分布，但只要确保dev数据集和测试数据集来自于同一分布，你的进度依然会很快。
最后，你可能不需要测试数据集，因为测试数据集是为了给你一个无偏的估计。但如果你不需要这种无偏的估计，你就不需要测试数据集。这种情况，很多人把dev数据集称之为测试数据集。这只是他们的一种说法，没办法纠正。
（没有解释什么时候不需要无偏估计）
"it is okay if you don't need a completely unbiased estimate of the performance of your algorithm."
my question is, under which circumstances you don't need a completely unbiased estimate?

