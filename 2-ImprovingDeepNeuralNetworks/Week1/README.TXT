1.Initializing
In general, initializing all the weights to zero results in the network failing to break symmetry. This means that every neuron in each layer will learn the same thing
初始化参数全部为0的时候，每一层的梯度变化的一样的，有就是每一层学习到的是一样的，就不会有比较好的结果

The cost starts very high. This is because with large random-valued weights, the last activation (sigmoid) outputs results that are very close to 0 or 1 for some examples, and when it gets that example wrong it incurs a very high loss for that example. Indeed, when  log(a[3])=log(0)log⁡(a[3])=log⁡(0) , the loss goes to infinity.
Poor initialization can lead to vanishing/exploding gradients, which also slows down the optimization algorithm.
If you train this network longer you will see better results, but initializing with overly large random numbers slows down the optimization.
当随机初始值比较大的时候，最后的输出sigmoid就是0或者1，这个时候如果碰见是0，那么计算lost的时候log(0)就是无限大，所以第一次迭代 Cost after iteration 0: inf
初始化参数过大会使开始训练的时候梯度下降得比较慢，Loss比较大，迭代会比较慢，当然最后也会收敛

Different initializations lead to different results
Random initialization is used to break symmetry and make sure different hidden units can learn different things
Don't intialize to values that are too large
He initialization works well for networks with ReLU activations.



2.regularization(L2 and Dropout)
一.L2和Dropout方法都是减少过拟合的方法，获得更小的参数
Conclusions
Regularization will help you reduce overfitting.
Regularization will drive your weights to lower values.
L2 regularization and Dropout are two very effective regularization techniques.

二.从实验结果来看，L2和Dropout都能获得比较好的准确率
model	train accuracy	test accuracy
3-layer NN without regularization	95%	91.5%
3-layer NN with L2-regularization	94%	93%
3-layer NN with dropout	93%	95%

三.L2
1.在原始J公式上加速正则化项，同时在backward计算的时候也需要加上正则化项，根据公式进行
2.J添加的正则化项是所有参数的L2之和
L2-regularization
L2-regularization relies on the assumption that a model with small weights is simpler than a model with large weights. Thus, by penalizing the square values of the weights in the cost function you drive all the weights to smaller values. It becomes too costly for the cost to have large weights! This leads to a smoother model in which the output changes more slowly as the input changes.

What you should remember -- the implications of L2-regularization on:
The cost computation:
A regularization term is added to the cost
The backpropagation function:
There are extra terms in the gradients with respect to weight matrices
Weights end up smaller ("weight decay"):
Weights are pushed to smaller values.

四.Dropout
1.一般输入层和输出层关闭dropout
2.如果某一层的某些单一shut down了，那么输出需要除以keep_prob，以保证激活函数和没有去掉神经元同样的输出
3.测试的时候需要关闭Dropout
What you should remember about dropout:
Dropout is a regularization technique.
You only use dropout during training. Don't use dropout (randomly eliminate nodes) during test time.
Apply dropout both during forward and backward propagation.
During training time, divide each dropout layer by keep_prob to keep the same expected value for the activations. For example, if keep_prob is 0.5, then we will on average shut down half the nodes, so the output will be scaled by 0.5 since only the remaining half are contributing to the solution. Dividing by 0.5 is equivalent to multiplying by 2. Hence, the output now has the same expected value. You can check that this works even when keep_prob is other values than 0.5.





3.Gradient & Checking
一.数值检测步骤
1.获得初始化参数
X, Y, parameters = gradient_check_n_test_case()

2.通过forward计算出cost和cache中间结果：a1，z1，w1，b1等
cost, cache = forward_propagation_n(X, Y, parameters)

3.通过forward得到的cache，再通过backward计算梯度
gradients = backward_propagation_n(X, Y, cache)

4.将初始化参数和backward得到的gradients，进行数值检测
difference = gradient_check_n(parameters, gradients, X, Y)



二.数值检测算法具体步骤
1.将所有参数视为vector，逐一改变每一个参数，得到一个改变后的参数列表，然后通过forward计算J_plus,J_minus
2.通过公式计算gradapprox,为一个向量
3.通过backward计算gradients,为一个向量
4.通过公式计算gradapprox与gradients的误差，看是否小于10e-(-7)


