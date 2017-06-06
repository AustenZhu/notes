...menustart

 - [Neural Networks](#6b347be0e79381eeb5689396d9e59438)
 - [Lecture 1](#b685b2632f64514a84fc8cbb0b4b7d2c)
	 - [Some simple models of neurons](#b02cb3fa93ab8f0e6485b0d13bc303cc)
		 - [Linear neurons](#1ed293fed5b9ae1cf9d961b5ce17cff8)
		 - [Binary threshold neurons](#60d743bd92d01784da86912ef3e9d3fa)
		 - [Rectified Linear Neurons](#bea9f293a1d10dc9a09ab31410552fc2)
		 - [Sigmoid neurons](#5dfb3a910337bd052071a460b50f17d7)
		 - [Stochastic binary neurons](#9fa3726b2244619bd1b4f0a6f3c0ad10)
 - [Lecture 2](#2cd2c77c9f81b7be54284357f2c55290)
	 - [Types of neural network architectures](#b553e95fb37e615918e131140aec36b1)
		 - [Feed-forward neural networks](#27403055d079f8f5057e91999fe9ff29)
		 - [Recurrent Networks](#3aa835dbc7f8ec8429d7671acae6aab5)
			 - [Recurrent neural networks for modeling sequences](#ab481de40578ba1e54e09346c919fe23)
			 - [An example of what recurrent neural nets can now do (to whet your interest!)](#ac843506e5b9c5acc3c517304fae2ab6)
		 - [Symmetrically connected networks](#bd53760cfb4568281010b21ad9f4c944)
	 - [A geometrical view of perceptrons](#b2f07d14cff56667ff8ce65beaa92ace)
		 - [Weight-space](#18fbaaed2b269781105b0c38d7d03d1f)
		 - [The cone of feasible solutions](#d70801a1a8a06ad3250060f4a42e0b7d)
	 - [What perceptrons can’t do](#f6493b60fa9aa860686d995485132458)
		 - [The limitations of Perceptrons](#8bac84924ecd4f05b2ef5fb5415cda08)
		 - [What binary threshold neurons cannot do](#14461318bc8dca1452e9768872689b06)
		 - [Learning with hidden units](#b984ea836f81bad4a3764c2908f793ec)
 - [Lecture 3](#28b761e5205ba2e17062ee27b6958d08)

...menuend


<h2 id="6b347be0e79381eeb5689396d9e59438"></h2>

# Neural Networks

<h2 id="b685b2632f64514a84fc8cbb0b4b7d2c"></h2>

# Lecture 1 

<h2 id="b02cb3fa93ab8f0e6485b0d13bc303cc"></h2>

## Some simple models of neurons 

<h2 id="1ed293fed5b9ae1cf9d961b5ce17cff8"></h2>

### Linear neurons

y = b + ∑ᵢ xᵢwᵢ

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_linear_neurons.png)

<h2 id="60d743bd92d01784da86912ef3e9d3fa"></h2>

### Binary threshold neurons 

 - First compute a weighted sum of the inputs
 - Then send out a fixed size spike of activity if the weighted sum exceeds a threshold. 


![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_bin_threshold_neurons.png)


![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_bin_threshold_neurons2.png)

<h2 id="bea9f293a1d10dc9a09ab31410552fc2"></h2>

### Rectified Linear Neurons

 - sometimes called linear threshold neurons
 - compute a **linear** weighted sum of their inputs.
 - The output **is a non-linear** function of the total input. 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_rectified_neurons.png)

<h2 id="5dfb3a910337bd052071a460b50f17d7"></h2>

### Sigmoid neurons 

 - give a real-valued output that is a smooth and bounded function of their total input. 
    - Typically they use the logistic function 
    - They have nice derivatives which make learning easy (see lecture 3). 

![][1]

<h2 id="9fa3726b2244619bd1b4f0a6f3c0ad10"></h2>

### Stochastic binary neurons 

 - These use the same equations as logistic units. 
    - But they treat the output of the logistic as the **probability** of producing a spike in a short time window.  
    

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_stochastic_bin_neurons.png)


---

<h2 id="2cd2c77c9f81b7be54284357f2c55290"></h2>

# Lecture 2

<h2 id="b553e95fb37e615918e131140aec36b1"></h2>

## Types of neural network architectures

<h2 id="27403055d079f8f5057e91999fe9ff29"></h2>

### Feed-forward neural networks

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_feedforward_nnet.png)

 - These are the commonest type of neural network in practical applications. 
    - The first layer is the input and the last layer is the output. 
    - If there is more than one hidden layer, we call them “deep” neural networks. 
 - They compute a series of transformations that change the similarities between cases
    - so at each layer, you get a new representation of the input , in which 
        - things that were similar in the previous layer may have become less similar
        - or things that were dissimilar in the previous layer may have become more similar
    - So in speech recognition, for example, we'd like the same thing said by different speaker to become more similar , and different things said by the same speaker to be less similar as we go up through the layers of the network
    - In order to achieve this, The activities of the neurons in each layer are a **non-linear** function of the activities in the layer below

<h2 id="3aa835dbc7f8ec8429d7671acae6aab5"></h2>

### Recurrent Networks 

 - These have directed cycles in their connection graph.
    - That means you can sometimes get back to where you started by following the arrows. 
 - They can have complicated dynamics and this can make them very difficult to train. 
    - There is a lot of interest at present in finding efficient ways of training recurrent nets. 
 - They are more biologically realistic. 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_recurrent_nnet.png)


 - Recurrent nets with multiple hidden layers are just a special case that has some of the hidden -> hidden connections missing. 

<h2 id="ab481de40578ba1e54e09346c919fe23"></h2>

#### Recurrent neural networks for modeling sequences

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_recurrent_nnet2.png)

 - Recurrent neural networks are a very natural way to model sequential data: 
    - They are equivalent to very deep nets(feed-forward)  with one hidden layer per time slice.
        - so at each time step , the states of the hidden units determines the states of the hidden units the next time step
    - Except that they use the same weights at every time slice and they get input at every time slice. 
        - this is one way they differ from feed-forward NNet. 
        - the weight matrix depicted by each red arrow is same at each time step
 - They have the ability to remember information in their hidden state for a long time. 
    - But its very hard to train them to use this potential.

<h2 id="ac843506e5b9c5acc3c517304fae2ab6"></h2>

#### An example of what recurrent neural nets can now do (to whet your interest!) 

 - Ilya Sutskever (2011) trained a special type of recurrent neural net to predict the next character in a sequence. 
 - After training for a long time on a string of half a billion characters from English Wikipedia, he got it to generate new text. 
    - It generates by predicting the probability distribution for the next character and then sampling a character from this distribution. 

<h2 id="bd53760cfb4568281010b21ad9f4c944"></h2>

### Symmetrically connected networks

 - These are like recurrent networks, but the connections between units are symmetrical (they have the same weight in both directions)
    - John Hopfield (and others) realized that symmetric networks are much easier to analyze than recurrent networks. 
    - They are also more restricted in what they can do. because they obey an energy function. 
        - **For example, they cannot model cycles**.
 - Symmetrically connected nets without hidden units are called “Hopfield nets”

---

<h2 id="b2f07d14cff56667ff8ce65beaa92ace"></h2>

## A geometrical view of perceptrons

perceptron is 二分类的线性分类模型。 输入为实例的特征向量，输出为实例的类别（取+1和-1）。


![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_perceptron_architecture.png)

<h2 id="18fbaaed2b269781105b0c38d7d03d1f"></h2>

### Weight-space

 - This space has one dimension per weight. 
 - A point in the space represents a particular setting of all the weights. 
    - 坐标系各个轴代表 wᵢ
 - Assuming that we have eliminated the threshold, each training case can be represented as a hyperplane through the origin. 
    - The weights must lie on one side of this hyper-plane to get the answer correct. 

--- 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_weight_space.png)

 - Each training case defines a plane (shown as a black line) 
    - The plane goes through the origin and is perpendicular to the **input vector**. 
        - input vector 就是 sample，training case 超平面 由它定义
        - input also represents constraints 
            - so we can think of the inputs as partitioning the space into 2 halves
            - weights lying in one half will get the answer corrent
            - the inputs will constrain the set of weights that give the correct classification result.
    - On one side of the plane the output is **wrong** because the scalar product of the weight vector with the input vector has the wrong sign. 
        - 同侧点积为正，异侧点积为负

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_weight_space2.png)


<h2 id="d70801a1a8a06ad3250060f4a42e0b7d"></h2>

### The cone of feasible solutions

 - To get all training cases right we need to find a point on the right side of all the planes. 
    - There may not be any such point! 
 - If there are any weight vectors that get the right answer for all cases, they lie in a hyper-cone with its apex at the origin. 
    - So the average of two good weight vectors is a good weight vector. 
        - **The problem is convex** 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_weight_space_con.png)

 - consider two inputs that both have a label of 1. we use a yellow arrow to represent a weight vectors which correctly classify the 2 inputs.
    - ![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_weight_space_con2.png)

<h2 id="f6493b60fa9aa860686d995485132458"></h2>

## What perceptrons can’t do 

<h2 id="8bac84924ecd4f05b2ef5fb5415cda08"></h2>

### The limitations of Perceptrons

 - If you are allowed to choose the features by hand and if you use enough features, you can do almost anything
    - For binary input vectors, we can have a separate feature unit for each of the exponentially many binary vectors and so we can make any possible discrimination on binary input vectors. (feature mapping ?)
        - This type of table look-up won’t generalize. 
 - But once the hand-coded features have been determined, there are very strong limitations on what a perceptron can learn.  

<h2 id="14461318bc8dca1452e9768872689b06"></h2>

### What binary threshold neurons cannot do 

 - A binary threshold output unit cannot even tell if two single bit features are the same! 
    - Positive cases (same): (1,1) -> 1; (0,0) -> 1 
    - Negative cases (different): (1,0) -> 0; (0,1) -> 0 
 - The four input-output pairs give four inequalities that are impossible to satisfy: 
    - w₁+w₂ >= θ , 0 >= θ
    - w₁<θ , w₂<θ 

<h2 id="b984ea836f81bad4a3764c2908f793ec"></h2>

### Learning with hidden units 

 - Networks without hidden units are very limited in the input-output mappings they can learn to model. 
    - More layers of linear units do not help. Its still linear. 
    - Fixed output non-linearities are not enough. 
 - We need multiple layers of **adaptive**,  non-linear hidden units. But how can we train such nets? 
    - We need an efficient way of adapting **all** the weights, not just the last layer.  This is hard.
    - Learning the weights going into hidden units is equivalent to learning features
    - This is difficult because nobody is telling us directly what the hidden units should do. 

---

<h2 id="28b761e5205ba2e17062ee27b6958d08"></h2>

# Lecture 3 

## Learning the weights of a linear neuron 

### Why the perceptron learning procedure cannot be generalised to hidden layers 
    
 - The perceptron convergence procedure works by ensuring that every time the weights change, they get closer to every “generously feasible” set of weights
    - This type of guarantee cannot be extended to more complex networks in which the average of two good solutions may be a bad solution
 - So “multi-layer” neural networks do not use the perceptron learning procedure
    - They should never have been called multi-layer perceptrons. 

### A different way to show that a learning procedure makes progress 

 - Instead of showing the weights get closer to a good set of weights, show that the actual output values get closer the target values. 
    - This can be true even for non-convex problems in which there are many quite different sets of weights that work well and averaging two good sets of weights may give a bad set of weights. 
    - It is not true for perceptron learning. 
 - The simplest example is a linear neuron with a squared error measure. 

### Linear neurons (also called linear filters) 

y = ∑<sub>ᵢ</sub> wᵢxᵢ = wᵀx 


 - The neuron has a realvalued output which is a weighted sum of its inputs 
 - The aim of learning is to minimize the error summed over all training cases. 
    - The error is the squared difference between the desired output and the actual output. 

### Why don’t we solve it analytically? 

 - 为什么不用矩阵直接求近似解？
 - Scientific answer: We want a method that real neurons could use. 
 - Engineering answer: We want a method that can be generalized to multi-layer, non-linear neural networks
    - The analytic solution relies on it being linear and having a squared error measure. 
    - Iterative methods are usually less efficient but they are much easier to generalize. 

### A toy example to illustrate the iterative method 

每天你在自助餐厅吃午饭。你的饮食包括鱼fish，薯条chips 和番茄酱ketchup 。每样你都会视心情拿几个。收银员只会告诉你膳食的总价格.几天后，您应该可以弄清每种食物的价格。

 - The iterative approach: 
    - Start with random guesses for the prices and
    - then adjust them to get a better fit to the observed prices of whole meals. 

### Solving the equations iteratively

 - price = x<sub>fish<sub>w<sub>fish<sub> + x<sub>chips<sub>w<sub>chips<sub> + x<sub>ketchup<sub>w<sub>ketchup<sub>
 - We will start with guesses for the weights w=( w<sub>fish<sub>, w<sub>chips<sub>, w<sub>ketchup<sub> )
    - and then adjust the guesses slightly
    - to give a better fit to the prices given by the cashier. 
 - The true weights used by the cashier
    - ![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_price_guess0.png)
 - A model of the cashier with arbitrary initial weights 
    - ![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_price_guess1.png)
    - Residual error = 350  
    - The “delta-rule” for learning is: 
        - Δwᵢ = εxᵢ(t-y) 
    - With a learning rate ε of 1/35 , the weight changes are 
        - +20, +50, +30 
    - This gives new weights of 70, 100, 80. 
        - Notice that the weight for chips got worse! 

### Deriving the delta rule 

 - Define the error as the squared residuals summed over all training cases: 
    - E = 1/2·∑<sub>n∈training</sub> (tⁿ-yⁿ)²
 - Now differentiate to get error derivatives for weights 
    - ![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_derive_delta_rule1.png)
 - The **batch** delta rule changes the weights in proportion to their error derivatives **summed
 over all training cases** 
    - ![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_derive_delta_rule2.png)
    - minus sign in front of ε cuz we want the error to go down.

### Behaviour of the iterative learning procedure 

 - Does the learning procedure eventually get the right answer? 
    - There may be no perfect answer. 
    - By making the learning rate small enough we can get as close as we desire to the best answer. 
 - How quickly do the weights converge to their correct values? 
    - It can be very slow if two input dimensions are highly correlated.
        - If you almost always have the **same number of** portions of ketchup and chips, it is hard to decide how to divide the price between ketchup and chips. 

     
### The relationship between the online delta-rule and the learning rule for perceptrons

 - In perceptron learning, we increment or decrement the weight vector by the input vector.
    - But we only change the weights when we make an error. 
 - In the online version of the delta-rule we increment or decrement the weight vector by the input vector scaled by the residual error and the learning rate. 
    - So we have to choose a learning rate. This is annoying. 

---

## The error surface for a linear neuron

### The error surface for a linear neuron 

 - The error surface lies in a space with
    - a horizontal axis for each weight
    - and one vertical axis for the error
 - For a linear neuron with a squared error, it is a quadratic bowl. 
    - Vertical cross-sections are parabolas 抛物线
    - Horizontal cross-sections are ellipses
    - ![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_error_surface.png)
 - For multi-layer, non-linear nets the error surface is much more complicated. 

### Online versus batch learning 

 - The simplest kind of batch learning does steepest descent on the error surface. 
    - This travels perpendicular to the contour lines. 
    - ![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_batch_error_surface.png)
 - The simplest kind of online learning zig-zags around the direction of steepest descent: 
    - This travels perpendicular to the training case line.
    - ![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_online_error_surface.png)

### Why learning can be slow 

 - If the ellipse is very elongated, the direction of steepest descent is almost perpendicular to the direction towards the minimum! 
    - The red gradient vector has a large component along the short axis of the ellipse and a small component along the long axis of the ellipse
    - This is just the opposite of what we want. 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_elongated_error_surface.png)

---

## Learning the weights of a logistic output neuron 

### Logistic neurons 

![][1]

They have nice derivatives which make learning easy


### The derivatives of a logistic neuron 

 - The derivatives of the logit, z, with respect to the inputs and the weights are very simple: 
    - ∂z/∂wᵢ = xᵢ
    - ∂z/∂xᵢ = wᵢ
 - The derivative of the output with respect to the logit is simple if you express it in terms of the output: 
    - dy/dz = y(1-y)

### Using the chain rule to get the derivatives needed for learning the weights of a logistic unit

 - To learn the weights we need the derivative of the output with respect to each weight: 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_sigmoid_error_derivative.png)

---

## The backpropagation algorithm 

### Learning with hidden units (again) 

 - Networks without hidden units are very limited 
 - Adding a layer of hand-coded features (as in a perceptron) makes them much more powerful but the hard bit is designing the features.
    - We would like to find good features without requiring insights into the task or repeated trial and error where we guess some features and see how well they work.  
 - We need to automate the loop of designing features for a particular task and seeing how well they work.

### Learning by perturbing weights

this idea occurs to everyone who knows about evolution

 - Randomly perturb one weight and see if it improves performance. If so, save the change. 
    - This is a form of reinforcement learning. 
    - **Very inefficient**. We need to do multiple forward passes on a representative set of training cases just to change one weight. Backpropagation is much better. 
    - Towards the end of learning, large weight perturbations will nearly always make things **worst** , because the weights need to have the right relative values

### Learning by using perturbations 

 - We could randomly perturb all the weights in parallel and correlate the performance gain with the weight changes. 
    - Not any better because we need lots of trials on each training case to “ see ” the effect of changing one weight through the noise created by all the changes to other weights.
 - A better idea: Randomly perturb the activities of the
 hidden units. 
    - Once we know how we want a hidden activity to change on a given training case, we can **compute** how to change the weights 
    - There are fewer activities than weights, but backpropagation still wins by a factor of the number of neurons. 

### The idea behind backpropagation

 - We don’t know what the hidden units ought to do, but we can compute how fast the error changes as we change a hidden activity.
    -  Instead of using desired activities to train the hidden units, use **error derivatives w.r.t. hidden activities**.
        - w.r.t :  with respect to
    - Each hidden activity can affect many output units and can therefore have many separate effects on the error. These effects must be combined. 
 - We can compute error derivatives for all the hidden units efficiently at the same time. 
    - Once we have the error derivatives for the hidden activities, its easy to get the error derivatives for the weights going into a hidden unit.  




### Sketch of the backpropagation algorithm on a single case 

 - First convert the discrepancy between each output and its target value into an error derivative. 
 - Then compute error derivatives in each hidden layer from error derivatives in the layer above. 
 - Then use error derivatives w.r.t.  activities to get error derivatives w.r.t. the incoming weights. 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_sketch_of_backpropagation.png)

### Backpropagating dE/dy

 - Backpropagation works with derivatives. It can be used for logistic neurons.  In a binary threshold neuron the derivatives of the output function are 0 , so the error singal will not be able to propagate through it. 



![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_Backpropagating_dEdy.png)

This is how you backpropagate the error derivative  with respect to the output of a unit. 

So we'll consider an output unit *j* and a hidden unit *i*. 

The output of the hidden unit i will be yᵢ , the output of the output unit j will be yⱼ. And the total input received by the output unit j will be zⱼ.

The first thing we need to do , is convert the error derivative with respect to yⱼ , into an error derivative with respect to zⱼ. 

To do that we use the chain rule.  As we've seen before, when we were looking at logistic units , it is showing as following: 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_Backpropagating_dEdy1.png)

So now we've got the error derivative with respect to the total input received by unit j. 

Now we can compute the error derivative with respect to the output of unit i -- yᵢ. It's gonna be the sum over all of the 3 outgoing connection of unit i. 

![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_Backpropagating_dEdy2.png)

So the first term there ( dzⱼ/dyᵢ )is how the total input to unit j (zⱼ) changes as we change the output of unit i (yᵢ). And then we have to multiply that by how the error root of changes as we change the totao input to unit j , which we can compute on the line above. 

And as we saw before , when studying the logistic unit, dzⱼ/dyᵢ is just the weight on the connection wᵢⱼ. 

So what we get is the error derivative with respect to the output of unit i (yᵢ) is sum of over all the outgoing connection to the layer above , of the weight wᵢⱼ on that connection times a quantity we would have already computed which is ∂E/∂zⱼ for the layer above. 

And so you can see the computation looks very like what we do on the forward pass, but we're going in the other direction. 

What we do for each unit in that hidden layer that contains i , is we compute the sum of a quantity in the layer above times  the weights on the connections. 

Once we've got ∂E/∂zⱼ , which we computed on the first line there, is very easy to get the error derivatives for all the weights coming into unity j. 


![](https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_Backpropagating_dEdy3.png)

∂zⱼ/∂wᵢⱼ is simply the activity of the unit in the layer below -- yᵢ. 

So the rule for changing the weight is just you multiply, this quantity you've computed at a unit ( ∂E/∂zⱼ) , by the activity coming in from the layer below. And that gives you the error of derivative with respect to weight. 


So on this slide we have seen how we can stop with  ∂E/∂zⱼ , and back propagate to get ∂E/∂zᵢ, we'll come backwards through one layer and computed the same quantity -- the derivative of the error with respect to the output in the previous layer. So we can clearly do that for as many layers as we like. And after we've done that for all these layers, we can compute how the error changes as you change the weights on the connections.  That's the backpropagation algorithm. It's an algorithm for taking 1 training case  and computing  efficiently , for every weight in the network , how the error will change , on that particular traning case ,  as you change the weight. 


---

∂E/∂wᵢⱼ = yᵢ·∂E/∂zⱼ =  yᵢ· yⱼ(1-yⱼ)·∂E/∂yⱼ = yᵢ· yⱼ(1-yⱼ)· -(tⱼ-yⱼ) 
 
let xᵢ = yᵢ

Δw = -ε(y-t) y(1-y)xᵢ


---


## Using the derivatives computed by backpropagation 

There are a number of other issues that have to be addressed before we actually get a learning procedure that's fully specified. For example , we need to decide how often to update the weights , and we need to decide how to prevent the network from over fitting very badly if we use a large network. 

### Converting error derivatives into a learning procedure 

 - The backpropagation algorithm is an efficient way of computing the error derivative ∂E/∂w for every weight on a single training case. 
 - To get a fully specified learning procedure, we still need to make a lot of other decisions about how to use these error derivatives: 
    - **Optimization issues:** How do we use the error derivatives on individual cases to discover a good set of weights?
    - **Generalization issues:** How do we ensure that the learned weights work well for cases we did not see during training? 
 - We now have a very brief overview of these two sets of issues.

### Optimization issues in using the weight derivatives 

 - How often to update the weights
    - **Online:** after each training case.
    - **Full batch:** after a full sweep through the training data.
    - **Mini-batch:** after a small sample of training cases. 
 - How much to update 
    - Use a fixed learning rate? 
    - Adapt the global learning rate? 
    - Adapt the learning rate on each connection separately? 
    - Don’t use steepest descent? 

### Overfitting: The downside of using powerful models

 - The training data contains information about the regularities in the mapping from input to output. But it also contains two types of noise. 
    - The target values may be unreliable (usually only a minor worry). 
    - There is **sampling error**. There will be accidental regularities just because of the particular training cases that were chosen. 
 - When we fit the model, it cannot tell which regularities are real and which are caused by sampling error. 
    - So it fits both kinds of regularity
    - – If the model is very flexible it can model the sampling error really well. **This is a disaster**.

### Ways to reduce overfitting

 - A large number of different methods have been developed. 
    - Weight-decay: try and keep the weights small , eg. try and keep many of the weights at 0 to make model simpler.
    - Weight-sharing: insist many of the weights have exactly the same value as each other
    - Early stopping: 
        - you make youself a  fake test set
        - as you're traning the net, you peak at what's happening on this fake test set. 
        - once the performance on the fake test set starting getting worse, you stop training 
    - Model averaging
        - you train lots of different nerual nets. 
        - and you average them together in the hopes that that will reduce the errors you're making
    - Bayesian fitting of neural nets
        - a fancy form of model averaging
    - Dropout
        - when you try and make your model more robust by randomly emitting hidden units when you're training it. 
    - Generative pre-training 

---

# Lecture 4: Learning to predict the next word




---

 [1]: https://raw.githubusercontent.com/mebusy/notes/master/imgs/NNet_sigmoid_neurons.png


