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
Conclusions
Regularization will help you reduce overfitting.
Regularization will drive your weights to lower values.
L2 regularization and Dropout are two very effective regularization techniques.


model	train accuracy	test accuracy
3-layer NN without regularization	95%	91.5%
3-layer NN with L2-regularization	94%	93%
3-layer NN with dropout	93%	95%



L2-regularization
L2-regularization relies on the assumption that a model with small weights is simpler than a model with large weights. Thus, by penalizing the square values of the weights in the cost function you drive all the weights to smaller values. It becomes too costly for the cost to have large weights! This leads to a smoother model in which the output changes more slowly as the input changes.

What you should remember -- the implications of L2-regularization on:
The cost computation:
A regularization term is added to the cost
The backpropagation function:
There are extra terms in the gradients with respect to weight matrices
Weights end up smaller ("weight decay"):
Weights are pushed to smaller values.



What you should remember about dropout:
Dropout is a regularization technique.
You only use dropout during training. Don't use dropout (randomly eliminate nodes) during test time.
Apply dropout both during forward and backward propagation.
During training time, divide each dropout layer by keep_prob to keep the same expected value for the activations. For example, if keep_prob is 0.5, then we will on average shut down half the nodes, so the output will be scaled by 0.5 since only the remaining half are contributing to the solution. Dividing by 0.5 is equivalent to multiplying by 2. Hence, the output now has the same expected value. You can check that this works even when keep_prob is other values than 0.5.



