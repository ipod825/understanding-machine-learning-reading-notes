# Chapter 2 - A Gentle Start

This chapter proves how machine learning can succeed. By making some assumptions, we will see that machine learning can learn a prediction rule (function) that makes small errors on both training data as well as real world data.

# A Formal Model – The Statistical Learning Framework
* The learner's input
    * Domain set $$\chi$$: A set of objects that we wish to label. Usually, this domain points are represented by a vector of features (e.g., several papayas represented by their color and softness).
    * Label set $$\mathcal{Y}$$: For current discussion, $$\mathcal{Y}$$ is restricted to a two-element set, $${0,1}$$ or $${-1,+1}$$ (e.g., whether the papaya is tasty or not).
    * Training data $$S=((x_1, y_1)\cdtts(x_m, y_m))$$: A finite sequence of pairs in $$\chi \times \mathcal{Y}$$; that is, a sequence of domain points and their labels. 

* The learner's output: A prediction rule (function) $$h:\chi \rightarrow \mathcal{Y}$$. The function is also called *predictor*, a *hypothesis*, or a *classifier*.

* How the training data $$S$$ is generated
    *  We assume that each instance $$x_i \in \Chi$$ is sampled accodrind to a probability distribution $$\mathcal{D}$$
    *  For current discussion, assume that there is a "correct" labeling function $$f: \chi \rightarrow \mathcal{Y}$$ such that $$y_i = f(x_i)$$ for all $$i$$.
    *  The laerner does not know anything about $$\mathcal{D}$$ and is required to learn $$f$$

* Meaures of Success
    * The error of a *classifier* is defined as the probability that it does not predict the correct label of a randomly sampled (according to $$ \mathcal{D}$$) data point.
    * Notation: Use the same notation of the distribution $$ \mathcal{D}$$ to denote a random variable
    * For an event $$A \subseteq \chi$$, $$ \mathcal{D}(A)$$ assigns a probability determing how likely it is to observe a point $$x \in A$$
    We then define the error of a prediction rule $$h:\chi \rightarrow \mathcal{Y}$$, to be
    $$L_{ \mathcal{D},f }(h) := \mathbb{P}_{x\sim \mathcal{D}}[h(x)\neq f(x)] := D({x: h(x)\neq f(x)})$$

