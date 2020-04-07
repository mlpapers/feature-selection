# Feature selection (variable selection)
> Feature selection is the process of selecting a subset of relevant features (variables, predictors) for use in model construction ([Wikipedia](https://en.wikipedia.org/wiki/Feature_selection))

Why feature selection?
1. Data exploration
2. Curse of dimensionality
3. Less features - faster models
4. Better metrics

- **Overview**
  - [An Introduction to Variable and Feature Selection](http://jmlr.csail.mit.edu/papers/volume3/guyon03a/guyon03a.pdf) (2003) *Isabelle Guyon, Andre Elisseeff*
  - [A Survey on Feature Selection](https://www.sciencedirect.com/science/article/pii/S1877050916313047) (2016) *Jianyu Miaoac, Lingfeng Niu*
  - [Feature Selection and Feature Extraction in Pattern Analysis: A Literature Review](https://arxiv.org/pdf/1905.02845.pdf) (2019) *Benyamin Ghojogh, Maria N. Samad, Sayema Asif Mashhadi,Tania Kapoor, Wahab Ali, Fakhri Karray, Mark Crowle*
- **All-relevant vs minimal-optimal feature selection**
  - [Consistent Feature Selection for Pattern Recognition in Polynomial Time](http://jmlr.csail.mit.edu/papers/volume8/nilsson07a/nilsson07a.pdf) (2007) *R. Nilsson, J. M. Peña, J. Björkegren, J. Tegnér*

### Filter methods
Filter methods use model-free ranking to filter less relevant features
- **Missing Values Ratio**
  - Removing features with a ratio of missing values greater than some threshold
- **Low Variance Filter** ([sklearn](https://scikit-learn.org/stable/modules/feature_selection.html#removing-features-with-low-variance))
  - Removing features with a variance lower than some threshold
- **Correlation** ([Wiki](https://en.wikipedia.org/wiki/Correlation_and_dependence))
- **χ²** Chi-squared statistic for categorical features ([Wiki](https://en.wikipedia.org/wiki/Chi-squared_test), [sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.chi2.html))
- **ANOVA** F-value for quantitative features([Wiki](https://en.wikipedia.org/wiki/Analysis_of_variance), [sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.f_classif.html))
- **Mutual information** ([Wiki](https://en.wikipedia.org/wiki/Mutual_information))
  - [Conditional Likelihood Maximisation: A Unifying Framework for Information Theoretic Feature Selection](http://jmlr.csail.mit.edu/papers/volume13/brown12a/brown12a.pdf) (2012) *Gavin Brown, Adam Pocock, Ming-Jie Zhao, Mikel Lujan*
  - [Feature Selection Based on Joint Mutual Information](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.41.4424) (1999) *Howard Hua Yang, John Moody*
  - [Estimating mutual information](https://arxiv.org/pdf/cond-mat/0305641.pdf) (2003) *Alexander Kraskov, Harald Stoegbauer, Peter Grassberger*
- **mRMR** Minimum redundancy, maximal relevancy ([Link](http://home.penglab.com/proj/mRMR/), [Wiki](https://en.wikipedia.org/wiki/Minimum_redundancy_feature_selection))
  - [Feature selection based on mutual information: criteria of max-dependency, max-relevance, and min-redundancy](http://home.penglab.com/papersall/docpdf/2005_TPAMI_FeaSel.pdf) (2005) *Hanchuan Peng, Fuhui Long, Chris Ding*
- **Relief** ([Wiki](https://en.wikipedia.org/wiki/Relief_(feature_selection)))
  - [The Feature Selection Problem: Traditional Methods and a New Algorithm](https://www.aaai.org/Papers/AAAI/1992/AAAI92-020.pdf) (1992) *Kira Kenji, Larry Rendell*
- **Markov Blanket** ([Wiki](https://en.wikipedia.org/wiki/Markov_blanket))
  - [Markov Blanket based Feature Selection: A Review of Past Decade](http://www.iaeng.org/publication/WCE2010/WCE2010_pp321-328.pdf) (2010) *Shunkai Fu, Michel C. Desmarais*
  - Incremental Association Markov Blanket: [Algorithms for Large Scale Markov Blanket Discovery](https://www.aaai.org/Papers/FLAIRS/2003/Flairs03-073.pdf) (2003) *Ioannis Tsamardinos, Constantin F. Aliferis, Alexander Statnikov*
  - Grow-Shrink algorithm: [Bayesian Network Induction via Local Neighborhoods](http://robots.stanford.edu/papers/Margaritis99a.pdf) (2000) *Dimitris Margaritis, Sebastian Thrun*
  - Koller-Sahami method: [Toward Optimal Feature Selection](http://ilpubs.stanford.edu:8090/208/1/1996-77.pdf) (1996) *Daphne Koller and Mehran Sahami*
  - Max-Min Markov Blanket: [Time and Sample Efficient Discovery of Markov Blankets and Direct Causal Relations](https://dl.acm.org/doi/10.1145/956750.956838) (2003) *Ioannis Tsamardinos, Constantin F. Aliferis, Alexander Statnikov*
- **Fast Correlation-based Filter**
  - [Feature Selection for High-Dimensional Data: A Fast Correlation-Based Filter Solution](https://www.public.asu.edu/~huanliu/papers/icml03.pdf) (2003) *Lei Yu, Huan Liu*
- **CBF** Consistency-Based Filters
  - [Consistency-based search in feature selection](https://www.public.asu.edu/~huanliu/papers/aij03.pdf) (2003) *Manoranjan Dasha, Huan Liu*
- **Interact**
  - [Searching for Interacting Features](https://www.public.asu.edu/~huanliu/papers/ijcai07.pdf) (2007) *Zheng Zhao, Huan Liu*

### Wrapper methods
Wrapper methods use a model and its performance to find the best feature subset
- **SFS** Sequential Feature Selection
- **SFFS** Sequential Floating Forward Selection
  - [Floating search methods in feature selection](https://www.academia.edu/15425286/Floating_search_methods_in_feature_selection) (1994) *Pavel Pudil, Josef Kittler, Jana Novovicová*
  - [Adaptive floating search methods in feature selection](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.11.5032) (1999) *P. Somol , Pavel Pudil , Jana Novovicova , P. Paclik*
- **Genertic algorithm** ([Wiki](https://en.wikipedia.org/wiki/Genetic_algorithm))
- **PSO** Particle Swarm Optimization ([Wiki](https://en.wikipedia.org/wiki/Particle_swarm_optimization))
  - [Particle Swarm Optimization](https://www.cs.tufts.edu/comp/150GA/homeworks/hw3/_reading6%201995%20particle%20swarming.pdf) (1995) *James Kennedy, Russell Eberhar*
  - [Feature Selection using PSO-SVM](http://www.iaeng.org/IJCS/issues_v33/issue_1/IJCS_33_1_18.pdf) (2007) *Chung-Jui Tu, Li-Yeh Chuang, Jun-Yang Chang, Cheng-Hong Yang*
- **Boruta** All-relevant feature selection ([CRAN](https://cran.r-project.org/web/packages/Boruta/), [PyPI](https://pypi.org/project/Boruta/))
  - [Boruta – A System for Feature Selection](https://www.mimuw.edu.pl/~ajank/papers/Kursa2010.pdf) (2010) *Miron B. Kursa,  Aleksander Jankowski,  Witold R. Rudnick*
- **MUVR** ([GitLab](https://gitlab.com/CarlBrunius/MUVR))
  - [Variable selection and validation in multivariate modelling](https://academic.oup.com/bioinformatics/article/35/6/972/5085367) (2018) *Lin Shi, Johan A Westerhuis, Johan Rosén, Rikard Landberg, Carl Brunius*
- Wrappers methods and overfitting:
  - [Wrappers for feature subset selection](http://machine-learning.martinsewell.com/feature-selection/KohaviJohn1997.pdf) (1996) *Ron Kohavi, George H. John*

### Embedded methods
- **LASSO**
  - [Regression Shrinkage and Selection via the lasso](https://statweb.stanford.edu/~tibs/lasso/lasso.pdf) (1996) *Robert Tibshirani*
- **Elastic net**
  - [Regularization and variable selection via the elastic net](https://web.stanford.edu/~hastie/Papers/B67.2%20(2005)%20301-320%20Zou%20&%20Hastie.pdf) (2005) *Hui Zou, Trevor Hastie*
- **Decision Tree** ([Wiki](https://en.wikipedia.org/wiki/Decision_tree))
- **Random Forest** ([Wiki](https://en.wikipedia.org/wiki/Random_forest))
  - [Random Forests](https://link.springer.com/article/10.1023/A:1010933404324) (2001) *Leo Breiman*
  - [Overview of Random Forest Methodology and Practical Guidance with Emphasis on Computational Biology and Bioinformatic](https://epub.ub.uni-muenchen.de/13766/1/TR.pdf) (2012) *Anne-Laure Boulesteix, Silke Janitza, Jochen Kruppa, Inke R. Konig*
  - [Variable selection using random forests](https://hal.archives-ouvertes.fr/hal-00755489/file/PRLv4.pdf) (2010) *Robin Genuer, Jean-Michel Poggi, Christine Tuleau-Malot*
  - [Bias in random forest variable importance measures: Illustrations, sources and a solution](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1796903/pdf/1471-2105-8-25.pdf) (2007) *Carolin Strobl, Anne-Laure Boulesteix, Achim Zeileis, Torsten Hothorn*
  - [Conditional Variable Importance for Random Forests](https://epub.ub.uni-muenchen.de/2821/1/deck.pdf) (2008) *Carolin Strobl, Anne-Laure Boulesteix, Thomas Kneib, Thomas Augustin, Achim Zeileis*
  - [Correlation and variable importance in random forests](https://arxiv.org/pdf/1310.5726.pdf) (2016) *Baptiste Gregorutti, Bertrand Michel, Philippe Saint-Pierre*
- **Gradient Boosting** ([Wiki](https://en.wikipedia.org/wiki/Gradient_boosting))
  - [Greedy Function Approximation: A Gradient Boosting Machine](https://statweb.stanford.edu/~jhf/ftp/trebst.pdf) (1999) *Jerome H Friedman*
  - [Boosting Algorithms as Gradient Descent](http://papers.nips.cc/paper/1766-boosting-algorithms-as-gradient-descent.pdf) (1999) *Llew Mason, Jonathan Baxter, Peter Bartlett, Marcus Frean*

### Unsupervised and semi-supervised feature selection
- **FSSEM** Feature Subset Selection using Expectation-Maximization
  - [Feature Selection for Unsupervised Learning](http://www.jmlr.org/papers/volume5/dy04a/dy04a.pdf) (2004) *Jennifer G. Dy, Carla E. Brodley*
- **Laplacian Score**
  - [Laplacian Score for Feature Selection](https://papers.nips.cc/paper/2909-laplacian-score-for-feature-selection.pdf) (2005) *Xiaofei  He, Deng  Cai, Deng Cai, Partha  Niyogi, Partha Niyogi*
- **Principal Feature Analysis**
  - [Feature Selection Using Principal Feature Analysis](http://venom.cs.utsa.edu/dmz/techrep/2007/CS-TR-2007-011.pdf) (2007) *Yijuan Lu, Ira Cohen, Xiang Sean Zhou, Qi Tian*
- **Spectral Feature Selection**
  - [Spectral Feature Selection forSupervised and Unsupervised Learning](https://www.public.asu.edu/~huanliu/papers/icml07.pdf) (2007) *Zheng Zhao, Huan Liu*
- **Autoencoders** ([Wiki](https://en.wikipedia.org/wiki/Autoencoder))
  - [Autoencoders, Unsupervised Learning, and Deep Architectures](http://proceedings.mlr.press/v27/baldi12a/baldi12a.pdf) (2012) *Pierre Baldi*
  - [An Introduction to Variational Autoencoders](https://arxiv.org/pdf/1906.02691.pdf) (2019) *Diederik P. Kingma, Max Welling*
  - [Concrete Autoencoders for Differentiable Feature Selection and Reconstruction](https://arxiv.org/pdf/1901.09346.pdf) (2019) *Abubakar Abid, Muhammad Fatih Balin, James Zou*

### Packages
- **R**
  - Package: fscaret ([CRAN](https://cran.r-project.org/web/packages/fscaret/)) *Jakub Szlek*
  - Package: praznik ([Code](https://gitlab.com/mbq/praznik)) *Miron Kursa*
  - Package: FSinR ([CRAN](https://cran.r-project.org/web/packages/FSinR/), [Paper](https://arxiv.org/pdf/2002.10330.pdf)) *Francisco Aragón-Royón, Alfonso Jiménez-Vílchez, Antonio Arauzo-Azofra, José Manuel Benítez*
  - Package: VSURF ([CRAN](https://cran.r-project.org/web/packages/VSURF/), [Paper](https://journal.r-project.org/archive/2015-2/genuer-poggi-tuleaumalot.pdf))
  - Package: spikeSlabGAM ([Code](https://github.com/fabian-s/spikeSlabGAM), [CRAN](https://cran.r-project.org/web/packages/spikeSlabGAM/), [Paper](https://www.jstatsoft.org/article/view/v043i14))
- **Python**
  - Package: sklearn.feature_selection
  - Package: feature-selector ([Code](https://github.com/WillKoehrsen/feature-selector), [PyPI](https://pypi.org/project/feature-selector/))


