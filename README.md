"# deeplearning-notes" 
# deeplearning-notes
* 　深度学习要调很多参数，没办法一次准确的猜测所有的参数，所以在实际应用中，这是一个高度迭代（very iterative）的过程，通常你是先有个idea，然后建一个神经网络，然后跑一下看看效果，根据结果来调整参数。通常一个领域的intuition并不会迁移到另一个领域。最优解可能取决于你拥有的数据量、特征数目、电脑配置、用GPU还是CPU。所以决定你的进度有多快的一个因素是你能多快地完成一轮迭代。
1. 合理地设置训练数据集、development数据集（hold-out cross validation set）和测试数据集的大小。
* 　我们在训练数据集上训练，在dev数据集上验证哪个模型表现最好并挑选模型，最终的结果用测试数据集评判。
* 　在以前通常划分为70%训练数据集，30%测试数据集，或者60%训练数据集，20%验证数据集（dev数据集），20%测试数据集。但在现在有大量的数据的时候，dev数据集和test数据集可以比例更小，因为dev数据集和存在的目的是测试哪个模型更好，所以他们只要足够大就行。比如有100万个样本，1万个样本足够用来判断哪个模型更好了。同样的test数据集的目的是给你一个关于模型有多好的无偏的估计。所以最终这一百万的数据可能划分为98万测试数据集，1万dev数据集，1万test数据集。
* 　另一个趋势是越来越多的人的训练数据集和测试数据集的分布不同。但吴恩达建议保证dev数据集和测试数据集的分布一致。由于deep learning对训练数据的需求是如此之大，很多时候我们会从各种来源搜集数据，因此即使训练数据集来自于不同的分布，但只要确保dev数据集和测试数据集来自于同一分布，你的进度依然会很快。
* 　最后，你可能不需要测试数据集，因为测试数据集是为了给你一个无偏的估计。但如果你不需要这种无偏的估计，你就不需要测试数据集。这种情况，很多人把dev数据集称之为测试数据集。这只是他们的一种说法，没办法纠正。（没有解释什么时候不需要无偏估计）
## my question
"it is okay if you don't need a completely unbiased estimate of the performance of your algorithm."
my question is, under which circumstances you don't need a completely unbiased estimate?

2. 偏差和方差
* 偏差和方差是机器学习里一个重要的概念，易学难精。即使你已经看过相关的定义，总有进一步理解的空间。
* 在深度学习领域已经很少谈及“偏差方差均衡”（bias-variance trade-off）。
* 首先我们来理解一下这两个概念：比如一个本应该用曲线隔开的两类点，如果我们只用线性模型拟合，这种类型就是高偏差，我们也称之为“欠拟合”，而与此相反，如果我们用一个无比复杂的分类器（比如深度神经网络），也许我们能正确的分类每一个样本点（包括噪声点），但这种分类器也“好”，这种类型就是高方差，也称之为“过拟合”。而中间类型的，既有一定程度的模型复杂度，也能区分出大多数点，则是一个“理想”的分类器。
* 理解偏差和方差的另一个方法就是训练误差和dev set error。比如图像识别，比如训练误差为1%，dev set error为11%，这表明你在训练数据集上表现良好，但在dev数据集上表现一般。所以看上去你在训练数据集上过拟合了，以至于你无法很好的在dev数据集上“泛化”（not generalizing well）。这种情形就是高方差。另一种情况，比如训练误差为15%，dev set error为16%，而普通人的误差接近于0%，则说明你的模型在训练数据集上表现也很差。也就是说你在训练数据集上“欠拟合”。这种情况就是高偏差。但这个模型的泛化能力并不算差，毕竟在dev set上的误差也就比训练数据集上多了1%。而如果在dev set上的误差为30%，则这个模型（吴恩达此处用的是algorithm，不是很理解为什么用这个词）也有高方差。
* 人类能达到的误差，或者最优误差（有时称之为贝叶斯误差）被当做基线（base）。如果基线就是15%，那么我们的分类器能有15%的误差也就是一个合理的误差了，此时就不能认为有15%的误差是高偏差。（比如很模糊的图片，人也不能高效地识别，更何况机器了）。
## my question
* classifer or algorithm?
* “So there's a classfier of high variance and this is overfitting the data.”So by looking at the training set error,you would be able to render a diagnosis of your algorithm having high variance."
