# Empirical Risk Minimization
Now, let's describe a simple learning paradigm for the preceding learning framework.

* Since the learner does not know both $$\mathcal{D}$$ and $$f$$, the true error $$L_{ \mathcal{D},f}(h)$$ is not available to the learner
* An alternative is the *training error*, the error the classifier incurs over the training sample, defined as:
> $$L_S(h) := \frac{|\{i \in [m]: h(x_i)\neq y_i\}|}{m}$$, where $$[m]=\{1,\dots,m\}$$
* The training error is also called *empericial error* or *empericial risk*
* Since the training sample $$S$$ is also sampled according to $$ \mathcal{D}$$, by minimizing the empirical risk $$L_S(h)$$, we hope we also minimize the true error $$L_{ \mathcal{D},f}(h)$$. 
* This learning paradigm – coming up with a predictor $$h$$ that minimizes $$L_S(h)$$ – is called *Empirical Risk Minimization* or ERM for short.

#### Something May Go Wrong – Overfitting
Remember the Pigeon Superstition Experiment? A pigeon in the cage is served with food at regular intervals. The pigeon wants more food and tries to repeat whatever chance actions happens at the food delivery time and such repetition reinforces the coincidence of the chance action and the food delivery. In the end, the pigeon keeps doing the same behavior and it feels satisfied because it found a prediction rule: "doing certain behavior leads to food delivery".

The pigeon is actually performing ERM, which minimizes the training error (though not defined accurately here). It found a predictor whose performance on the training set is excellent, yet its performance on the true “world” is very poor. This phenomenon is called overfitting. Intuitively, overfitting occurs when our hypothesis fits the training data “too well”. A more formal example is described in section 2.2.1 in the book.

