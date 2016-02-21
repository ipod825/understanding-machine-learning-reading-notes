# Empirical Risk Minimization with Inductive Bias
In this section, we formal prove that we are able to avoid overfitting by
1. limiting the number of possible hypothesis and
2. by increasing the number of training data.

#### Finite Hypothesis Class
* A common solution to avoid overfitting is to restrict the search space of ERM
* Formally, the learner should choose in advance (before seeing the data) a set of predictors $$ \mathcal{H}$$, called a *hypothesis class*
* For a given hypothesis class $$ \mathcal{H}$$ and a training sample $$S$$, the $$ERM_{ \mathcal{H} }$$ learner choose a predictor $$h \in \mathcal{H}$$, with the lowest possible error over $$S$$. Formally,
> $$ERM_{ \mathcal{H} }(S) \in \mathop{argmin}_{h \in \mathcal{H}} L_s(h)$$ [^1]
* By restricting the learner to choosing a predictor from $$\mathcal{H}$$, we bias it toward a particular set of predictors. Such restrictions are often called an *inductive bias*
* The restriction is determined before the learner sees the training data, it should ideally be based on some prior knowledge about the problem to be learned
* For example, for the papaya taste prediction problem we may choose the class $$\mathcal{H}$$ to be the set of predictors that are determined by axis aligned rectangles (in the space determined by the color and softness coordinates) 
* A fundamental question in learning theory is, over which hypothesis classes, will $$ERM_{ \mathcal{H}}$$ not result in overfitting
* Intuitively, choosing a more restricted hypothesis class better protects us against overfitting but at the same time might cause us a stronger inductive bias


#### Derivation of Overfitting
In the following, we will prove that we are able to avoid overfitting by having finite hypothesis claas and sufficiently large training sample. The intuition is as follows:
1. We write down the probability of overfitting and set an inequality equation to upper bound on it 
2. By solving the inequality equation, we derive the number of samples required to avoid overfitting at certain confidence level

We will have two assumptions for the following derivation:
1. The Realizability Assumption: There exists $$h^* \in \mathcal{H}$$ $$s.t.$$ $$L_{\mathcal{D},f}(h^*)=0$$. That is, we can always find a hypothesis in $$ \mathcal{H}$$ such that the true error is zero. 
2. The i.i.d. Assumption: The examples in the training set are independently and identically distributed (i.i.d.) according to the distribution $$ \mathcal{D}$$. We denote this assumption by $$S\sim \mathcal{D^m}$$ [^2]
 

Note that the first assumptions implies $$ERM_{ \mathcal{H} }$$ can always find a hypothesis that leads to zero empirical risk. However, since there might be multiple hypothesis that leads to zero empirical risk, $$h^*$$ is not guaranteed to be selected. Therefore, we will not face underfitting (training error too high) but we are still at the risk of overfitting.

Now, let's derive the magic
* $$ERM_{ \mathcal{H}}(S)$$ gives us a hypothesis $$h_S \in \mathop{argmin}_{h \in \mathcal{H}} L_s(h)$$. By assumption 1, $$L_s(h_s)=0$$ 
* Overfitting happens when the true error is greater than a certain amount $$\epsilon$$.
> $$L_{ \mathcal{D},f(h_s) > \epsilon}$$
* Since $$h_s$$ depends on the training set $$S$$, which is picked by a random process.
* Hence, the true error is a random variable, and the probability that overfitting happens is 
> $$ \mathbb{P}[L_{ \mathcal{D},f(h_s)} > \epsilon] = \mathcal{D}^m(\{S|_x: L_{ \mathcal{D},f }(h_s)>\epsilon\})$$
* We than upperbound the probability of overfitting with a parameter $$\delta$$
> $$ \mathcal{D}^m(\{S|_x: L_{ \mathcal{D},f }(h_s)>\epsilon\})<\delta$$,
where $$S|_x=(x_1\dots, \x_m)$$ is the instances of the training set

Another interpretation of overfitting is that we are very unlucky to get a nonrepresentative sample that leads to great true error. What we want to do is to bound the probability of such "unluckiness" to a small value $$\delta$$.

Now we have the inequality equation. Let's solve it to derive our conclusion.

First, let's see when will a nonrepresentative sample that leads to overfitting happens? By assumption 1, $$ERM_{ \mathcal{H} }$$ always chosse hypothesis that leads to zero empirical error $$L_s(h_s)=0$$. It follows that if overfitting happens, both $$L_{ \mathcal{D},f(h_s)>\epsilon}$$ and $$L_s(h_s)=0$$ will hold. That is, a hypothesis $$h$$ is a potential "bad" hypothesis it in the set $$ \mathcal{H}_ \in \{\}$$

Formally, let $$ \mathcal{H}_B$$ be the set of "bad" hypothesis
> $$ \mathcal{H}_B = \{h \in \mathcal{H}: L_{ \mathcal{D},f }(h)>\epsilon\}$$ 



and let $$M$$ be the misleading samples
> $$M = {S|_x: \exists h \in \mathcal{H}_B, L_S(h)=0 }$$



First, let's review the overfitting process again. By assumption 1, $$ERM_{ \mathcal{H} }$$ first chose an hypothesis $$h_s$$ such that the empirical risk $$L_s(h_s)=0$$, but unfortunately the true error $$L_{ \mathcal{D},f(h_s)>\epsilon}$$. Therefore, we know that for a hypothesis $$h$$ to lead to overfitting, 

First, let's see the misleading samples, $$ S_B = {S|_x: L_{ \mathcal{D},f(h_s)>\epsilon}$$. One thing to notice is that $$S_B$$ depends on the implementation of $$ERM_{ \mathcal{H} }$$. Imaging that we assign a index to each possible sample for $$m$$-tuple. For one implementation of $$ERM_{ \mathcal{H} }$$, $$S_B$$ might contain the $$1^{st},3^{rd}\dots$$ samples, and for another implementation, $$S_B$$ might contain the $$2^{nd},4^{th}\dots$$ samples.

Since we are making no assumption on the implementation of $$ERM_{ \mathcal{H} }$$, the best we can do is to take the union of all possible $$S_B$$. Formally, let $$ \mathcal{H}_B$$ be the set of "bad" hypothesis
> $$ \mathcal{H}_B = \{h \in \mathcal{H}: L_{ \mathcal{D},f }(h)>\epsilon\}$$ 

and let $$M$$ be the misleading samples
> $$M = {S|_x: \exists h \in \mathcal{H}_B, L_S(h)=0 }$$

For every  $$S|_x \in M $$ there is a "bad" hypothesis, $$h \in \mathcal{H}_B$$ that could be selected by our $$ERM_{ \mathcal{H} }$$ algorithms (since by assumption 1, $$ERM_{ \mathcal{H} }$$ will select a hypothesis that leads to zero training error)

* The simplest type of restriction on a class is imposing an upper bound on its size (that is, the number of predictors $$h$$ in \mathcal{H}).

* Denote the probability of getting (which leads to overfitting) by $$\delta$$, and call $$(1-\delta)$$  the *confidence parameter* of our prediction

[^1]: There might be multiple $$h$$ leading to the minimum error on $$S$$.
[^2]: Like $$ \mathcal{D}(A)$$, $$ \mathcal{D}^m(A^m)$$ assigns a probability determining how likely it is to observe a sequence of sample belonging to the event $$A^m \subseteq \chi^m$$






