## The Statistical Learning Framework
Let's first describe a formal model capturing statistical learning tasks.

### The Learner's Input
* Domain set $$\chi$$: A set of objects that we wish to label. Usually, this domain points are represented by a vector of features (e.g., several papayas represented by their color and softness).
* Label set $$\mathcal{Y}$$: For current discussion, $$\mathcal{Y}$$ is restricted to a two-element set, $$\{0,1\}$$ or $$\{-1,+1\}$$ (e.g., whether the papaya is tasty or not).
* Training data $$S=((x_1, y_1)\dots(x_m, y_m))$$: A finite sequence of pairs in $$\chi \times \mathcal{Y}$$; that is, a sequence of domain points and their labels.

### How the Training Data $$S$$ is Generated
* We assume that each instance $$x_i \in \chi$$ is sampled according to a probability distribution $$\mathcal{D}$$
* For current discussion, assume that there is a "correct" labeling function $$f: \chi \rightarrow \mathcal{Y}$$ such that $$y_i = f(x_i)$$ for all $$i$$.


### The Learner's Output
* The learner does not know anything about $$\mathcal{D}$$ and is required to learn $$f$$
* The learner should output a prediction rule (function) $$h:\chi \rightarrow \mathcal{Y}$$. The function is also called *predictor*, a *hypothesis*, or a *classifier*.

### Measures of Success
* The error of a *classifier* is defined as the probability that it does not predict the correct label of a randomly sampled (according to $$ \mathcal{D}$$) data point.
* Formally, the error of the classifier $$h:\chi \rightarrow \mathcal{Y}$$ is defined as  
$$L_{ \mathcal{D},f }(h) \mathop{=}^{def} \mathop{\mathbb{P}}_{x\sim \mathcal{D}}[h(x)\neq f(x)] \mathop{=}^{def} \mathcal{D}(\{x: h(x)\neq f(x)\})$$. 
* The notation $$ \mathcal{D}(A)$$ assigns a probability determining how likely it is to observe a point $$x \in A$$, where $$A \subseteq \chi$$ is an event.
* In other words, with respect to the distribution $$ \mathcal{D}$$ and the correct labeling function $$f$$, the error of such $$h$$ is the probability of a randomly sampled example $$x$$ belonging to the set $$\{x| h(x)\neq f(x)\}$$
* $$L_{ \mathcal{D},f }(h)$$ is also called the *genralization error*, the *risk*, the *true error* of $$h$$
* The letter $$L$$ is used since we view the error as a *loss* of the learner.
