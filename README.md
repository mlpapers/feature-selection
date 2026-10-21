# Feature Selection and Variable Selection

## Selection objectives

- **Predictive selection:** chooses a small or inexpensive input subset for a specified learner and prediction task. Its risk–cost trade-off need not identify a unique set of generating variables. [Overview](https://jmlr.org/papers/v3/guyon03a.html).
- **Minimal-optimal versus all-relevant:** a small subset sufficient for prediction and the full set of relevant variables are different targets; redundant variables can matter to the latter. [Nilsson et al.](https://jmlr.org/papers/v8/nilsson07a.html) (2007).
- **Conditional discovery:** model-X knockoffs test whether the target is independent of a variable given all remaining inputs. This target differs from keeping every useful substitute. [Model-X](https://arxiv.org/abs/1610.02351).
- **Unsupervised selection:** usefulness is defined by a chosen surrogate, such as reconstruction, neighborhoods or cluster structure. Preserving it does not establish utility for an unspecified target. [Survey](https://arxiv.org/abs/1601.07996).
- **Acquisition:** static selection uses one subset; an adaptive policy chooses the next measurement from values already observed. This differs from selecting an explanation after seeing all inputs. [Dynamic selection](https://proceedings.mlr.press/v202/covert23a.html).

### Interactions and interchangeable variables

- **XOR example:** for independent fair bits, Y = X1 XOR X2 is independent of either input alone, yet determined by their pair. Even nonlinear univariate dependence scores can miss joint information. [Selection criteria](https://jmlr.org/papers/v13/brown12a.html).
- **Duplicate example:** if X1 = X2 = Y, either input predicts perfectly, and each is conditionally uninformative given the other. Changing between these subsets need not change predictions. [Multiple boundaries](https://jmlr.org/papers/v14/statnikov13a.html).

## Comparative evidence

- **Tabular deep-learning benchmark — NeurIPS 2023:** on 12 datasets with MLP/FT-Transformer predictors, the authors report Deep Lasso gains on corrupted and second-order added features. Evidence is specific to those regimes. [Study](https://arxiv.org/html/2311.05877v1).
- **Added features need not be irrelevant:** products of original variables can help prediction. The 2023 benchmark evaluates downstream quality; rejecting every added column would reward the wrong objective. [§5](https://arxiv.org/html/2311.05877v1).
- **SelectArena — 2026 preprint:** across 71 datasets and five learners, tree importance and F-tests offer strong prediction/runtime trade-offs; F-tests also rank highly on stability and noise rejection. [v2, §4](https://arxiv.org/abs/2610.13644v2).
- **SelectArena protocol:** enforces exactly k features and a one-hour selection budget. Interrupted searches use random filling or subsampling; reported search rankings include this fallback. [v2, §3.3 and Appendix D.2](https://arxiv.org/pdf/2610.13644v2).
- **SelectArena metrics:** “validity” measures rejection of injected Gaussian-noise columns; it does not establish relevance of every retained original feature. Reported improvement over random subsets uses that comparator. [v2, §3.3](https://arxiv.org/pdf/2610.13644v2).
- **Comparison design:** use all-feature prediction, random subsets at matched budgets and simple filters as baselines. Report prediction, subset size/cost, selection time and stability separately. [Benchmark](https://arxiv.org/pdf/2610.13644v2).

## Filter criteria and screening

### Marginal screening

- **Variance threshold:** removes features with low training-set variance without using labels; scale affects the result. [scikit-learn](https://scikit-learn.org/stable/modules/feature_selection.html#removing-features-with-low-variance).
- **Univariate tests:** [chi-squared](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.chi2.html) for non-negative counts/frequencies; [ANOVA F](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.f_classif.html) for class differences; [linear-regression F](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.f_regression.html) for marginal linear association. Individual scores can miss interactions.
- **Sure independence screening (SIS/ISIS):** screens marginal correlations before subset fitting; ISIS repeats screening. Signal/design assumptions give high-probability retention of all signals, while extra variables may remain. [Fan–Lv](https://arxiv.org/abs/math/0612857) (2006/2008).

### Information, redundancy, and interactions

- **Mutual information:** a dependence quantity; [Kraskov et al.](https://arxiv.org/abs/cond-mat/0305641) (2003/2004) provide an estimator. mRMR/JMI define selection criteria, while forward search constructs a subset. These are separate choices. [Framework](https://jmlr.org/papers/v13/brown12a.html).
- **MI estimation:** discrete and continuous features require appropriate treatment; mislabeling their type can give incorrect estimates. Nonlinear dependence estimation does not make marginal scoring interaction-aware. [scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.mutual_info_classif.html).
- **mRMR:** balances feature–target mutual information against redundancy among selected features. [Peng, Long, Ding](https://doi.org/10.1109/TPAMI.2005.159) (2005).
- **Joint mutual information (JMI):** scores candidates jointly with already selected variables. [Yang and Moody](https://proceedings.neurips.cc/paper_files/paper/1999/hash/8c01a75941549a705cf7275e41b21f0d-Abstract.html) (1999); [Brown et al.](https://jmlr.org/papers/v13/brown12a.html) (2012) derive JMI and related criteria as approximations to conditional-likelihood selection.
- **FCBF — fast correlation-based filter:** uses symmetrical uncertainty to screen relevance and remove redundant features. [Yu and Liu](https://www.aaai.org/Papers/ICML/2003/ICML03-111.pdf) (2003).
- **Relief:** updates feature weights from nearby same-class and different-class examples. [Kira and Rendell](https://www.aaai.org/Papers/AAAI/1992/AAAI92-020.pdf) (1992); [Relief-family review](https://arxiv.org/abs/1711.08421) (2017/2018) covers interaction sensitivity and extensions.
- **Consistency-based selection:** penalizes identical selected-feature patterns with conflicting labels. [Dash and Liu](https://doi.org/10.1016/S0004-3702(03)00079-1) (2003) compare search strategies using this criterion.
- **INTERACT:** removes features using changes in class inconsistency, targeting interactions that marginal ranking can miss. [Zhao and Liu](https://www.ijcai.org/Proceedings/07/Papers/187.pdf) (2007).

## Conditional independence and Markov boundaries

- **[FOCI](https://arxiv.org/abs/1910.12327)** — 2019/2021. Greedily adds variables using a conditional-dependence statistic. Its sufficient-set recovery result needs detectable improvement at every insufficient subset; purely joint signals can defeat this forward-search condition.
- **Markov blankets:** seek variables that render the target conditionally independent of the remaining variables. Discovery depends on conditional-independence tests and distributional assumptions. [Fu and Desmarais review](https://www.iaeng.org/publication/WCE2010/WCE2010_pp321-328.pdf) (2010).
- **Markov boundary:** an inclusion-minimal blanket. Multiple boundaries can exist, yielding alternative sufficient subsets; disagreement need not identify a uniquely wrong selection. [Statnikov et al.](https://jmlr.org/papers/v14/statnikov13a.html) (2013).
- **Koller–Sahami:** eliminates features using approximate Markov blankets and information-theoretic redundancy criteria. [Toward Optimal Feature Selection](https://ai.stanford.edu/~koller/Papers/Koller+Sahami:ICML96.pdf) (1996).
- **Grow–Shrink:** grows a candidate blanket and then removes conditionally irrelevant variables. [Margaritis and Thrun](https://robots.stanford.edu/papers/Margaritis99a.pdf) (1999/2000).
- **IAMB:** incremental association-based blanket discovery, with forward inclusion and backward pruning. [Tsamardinos, Aliferis, Statnikov](https://aaai.org/papers/flairs-2003-073/) (2003).
- **Max–Min blanket discovery:** identifies parents/children and extends the search to a target's Markov blanket. [Tsamardinos et al.](https://doi.org/10.1145/956750.956838) (2003). A predictive blanket alone does not identify causal direction.

## Subset search and cardinality optimization

- **Wrappers:** evaluate candidate subsets using a particular learner's predictive performance. Search and validation are part of the method. [Kohavi and John](https://machine-learning.martinsewell.com/feature-selection/KohaviJohn1997.pdf) (1997).
- **Sequential selection:** greedily adds or removes features according to cross-validation scores. [SequentialFeatureSelector](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.SequentialFeatureSelector.html) supports forward and backward search.
- **Floating search:** alternates inclusion and exclusion to revisit earlier choices. [Pudil, Novovičová, Kittler](https://doi.org/10.1016/0167-8655(94)90127-9) (1994); [adaptive floating search](https://doi.org/10.1016/S0167-8655(99)00083-5) (1999) varies the search depth.
- **Recursive feature elimination (RFE):** repeatedly fits a model and removes low-ranked inputs. [SVM-RFE](https://doi.org/10.1023/A:1012487302797) (2002); [RFE](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.RFE.html) and [RFECV](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.RFECV.html) implement elimination and cross-validated subset-size selection.
- **Population-based subset search:** [genetic search](https://doi.org/10.1016/j.procs.2016.07.111) and [particle swarms](https://www.cs.tufts.edu/comp/150GA/homeworks/hw3/_reading6%201995%20particle%20swarming.pdf) explore subsets scored by a chosen criterion; that criterion defines the selection objective. [PSO–SVM application](https://www.iaeng.org/IJCS/issues_v33/issue_1/IJCS_33_1_18.pdf) (2007).
- **Best-subset optimization:** mixed-integer formulations constrain feature count directly. Solver bounds can certify global optimality or quantify a remaining gap when stopped early. [Bertsimas et al.](https://arxiv.org/abs/1507.03133) (2015).
- **Fast L0 selection:** coordinate descent and local combinatorial search optimize L0-penalized objectives. Their local optimality conditions differ from a global MIO certificate. [Hazimeh–Mazumder](https://arxiv.org/abs/1803.01454) (2018/2020).

## Embedded sparsity and model-based selection

### Penalized and Bayesian models

- **Lasso:** an L1 penalty yields sparse regression coefficients, coupling variable selection with fitting. [Tibshirani](https://doi.org/10.1111/j.2517-6161.1996.tb02080.x) (1996).
- **[Adaptive lasso](https://doi.org/10.1198/016214506000000735)** — 2006. Weights each coefficient’s L1 penalty using an initial estimate. Zou establishes selection consistency and oracle asymptotics under design, initialization and tuning conditions; this is not a finite-sample guarantee of correct support.
- **Lasso support recovery:** sparse prediction does not establish correct variable recovery. Selection consistency requires additional assumptions, notably restrictions on predictor dependence. [Zhao–Yu](https://jmlr.org/papers/v7/zhao06a.html) (2006).
- **Elastic net:** combines L1 and L2 penalties, encouraging groups of correlated predictors to enter together. [Zou and Hastie](https://web.stanford.edu/~hastie/Papers/B67.2%20(2005)%20301-320%20Zou%20&%20Hastie.pdf) (2005).
- **Group lasso:** selects predefined groups of coefficients, such as all encoded levels of a categorical variable. [Yuan and Lin](https://doi.org/10.1111/j.1467-9868.2005.00532.x) (2006). This differs from elastic net's grouping of correlated predictors.
- **Spike-and-slab:** mixture priors represent exclusion and inclusion of regression coefficients. [Mitchell and Beauchamp](https://doi.org/10.1080/01621459.1988.10478694) (1988); [George and McCulloch](https://faculty.wharton.upenn.edu/wp-content/uploads/2012/04/Approaches-for-bayesian-variable-selection.pdf) (1997) develop computational approaches.
- **[HSIC Lasso](https://arxiv.org/abs/1202.0515)** — 2012. Uses feature-wise kernels to select variables with strong nonlinear dependence on the response and limited redundancy with one another; a sparse alternative to linear Lasso screening.

### Trees, importance, and subset rules

- **Decision trees:** split-based importance sums impurity reductions attributed to each input; thresholding can select a subset. [Importance definition](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html), [subset rule](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.SelectFromModel.html). These scores can favor high-cardinality inputs.
- **Random forests:** ensembles provide importance scores used for ranking and selection. [Breiman](https://doi.org/10.1023/A:1010933404324) (2001); [Boulesteix et al.](https://epub.ub.uni-muenchen.de/13766/1/TR.pdf) (2012) review practical pitfalls. A ranking still needs a subset-selection rule.
- **Gradient boosting:** sequential function fitting can supply feature-importance rankings. [Friedman](https://doi.org/10.1214/aos/1013203451) (2001); [functional-gradient interpretation](https://papers.nips.cc/paper/1766-boosting-algorithms-as-gradient-descent.pdf) (1999). [Importance thresholding](https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.SelectFromModel.html) produces a subset.
- **Boruta:** targets all-relevant selection by comparing random-forest importances with randomized shadow features. [Algorithm](https://www.mimuw.edu.pl/~ajank/publications/kursa-boruta-2010/Kursa2010.pdf) (2010); [R package paper](https://www.jstatsoft.org/article/view/v036i11), [Python](https://github.com/scikit-learn-contrib/boruta_py).
- **VSURF:** forest importance and stepwise selection produce subsets for interpretation and prediction. [Genuer, Poggi, Tuleau-Malot](https://hal.archives-ouvertes.fr/hal-00755489/file/PRLv4.pdf) (2010); [VSURF package](https://doi.org/10.32614/RJ-2015-018) (2015).

### Differentiable selectors

- **Concrete autoencoders:** learn which original inputs to retain through a relaxed discrete selector and reconstruction decoder. [Paper](https://proceedings.mlr.press/v97/balin19a.html) (ICML 2019); [code](https://github.com/mfbalin/Concrete-Autoencoders).
- **Stochastic gates (STG):** learn input gates jointly with a predictor using a continuous relaxation of an L0 feature-count penalty. [Paper](https://proceedings.mlr.press/v119/yamada20a.html) (ICML 2020); [code](https://github.com/runopti/stg).
- **LassoNet:** ties nonlinear feature use to sparse linear skip connections through a hierarchical constraint; produces a regularization path of global subsets. [Paper](https://jmlr.org/papers/v22/20-848.html) (2021); [code](https://github.com/lasso-net/lassonet).
- **Deep Lasso:** applies a group penalty to loss gradients with respect to input features, extending linear sparsity to input sensitivity. Gradient norms also rank features. [Method, §6](https://arxiv.org/html/2311.05877v1) (2023).

## Unsupervised and graph-based selection

- **FSSEM:** searches feature subsets alongside expectation-maximization clustering; examines likelihood and scatter criteria and their dimensionality biases. [Dy and Brodley](https://jmlr.org/papers/v5/dy04a.html) (2004).
- **Laplacian Score:** ranks features by preservation of local graph structure; applicable without class labels. [He, Cai, Niyogi](https://papers.nips.cc/paper/2909-laplacian-score-for-feature-selection.pdf) (2005).
- **Principal feature analysis:** uses PCA-derived structure to choose representative original variables. [Lu et al.](https://doi.org/10.1145/1291233.1291297) (2007). Its output is an input subset rather than principal-component coordinates.
- **Spectral feature selection (SPEC):** evaluates features through a similarity graph's spectrum, covering supervised and unsupervised criteria. [Zhao and Liu](https://doi.org/10.1145/1273496.1273641) (2007).
- **Multi-cluster feature selection (MCFS):** combines a spectral embedding with sparse regression to select features preserving cluster structure. [Cai, Zhang, He](https://doi.org/10.1145/1835804.1835848) (2010).

## Resampling, error control and post-selection inference

- **Stability selection:** thresholds selection frequencies across subsamples. Its original bound controls the expected number of false selections under exchangeability and other assumptions. [Meinshausen and Bühlmann](https://arxiv.org/abs/0809.2932) (2008/2010).
- **Complementary-pairs stability selection:** pairs disjoint half-samples and bounds selection of variables with low selection probabilities, without the original exchangeability requirement. [Shah and Samworth](https://arxiv.org/abs/1105.5578) (2011/2013).
- **Knockoff+:** selects against synthetic control variables with finite-sample false discovery rate control in the paper's Gaussian linear-model setting. [Barber and Candès](https://arxiv.org/abs/1404.5609) (2014/2015).
- **Model-X knockoffs:** permits arbitrary response models; FDR control requires exchangeability and knockoffs independent of the response conditional on the inputs. [Candès et al.](https://arxiv.org/abs/1610.02351) (2016/2018); [software](https://web.stanford.edu/group/candes/knockoffs/).
- **Knockoff robustness:** flexibility in the response model relies on modeling the input distribution. Errors in estimated feature conditionals can inflate FDR; robustness bounds quantify this dependence. [Barber et al.](https://arxiv.org/abs/1801.03896) (2018).
- **Artificial controls, different targets:** [Boruta](https://www.jstatsoft.org/article/view/v036i11) compares forest importances with shuffled shadows for all-relevant selection; [model-X](https://arxiv.org/abs/1610.02351) uses exchangeable controls for conditional discovery with FDR control under its assumptions.
- **Ensemble selection:** aggregates feature preferences across perturbed datasets or selectors. [Saeys, Abeel, Van de Peer](https://biblio.ugent.be/publication/535025) (2008); [bootstrap/fuzzy-set aggregation](https://arxiv.org/abs/2005.05003) (2020). Aggregation alone supplies no generic FDR guarantee.
- **[Deep knockoffs](https://arxiv.org/abs/1811.06687)** — 2018. Learns approximate model-X knockoff generators by encouraging pairwise exchangeability. Generator diagnostics matter: approximate sampling alone does not establish exact false-discovery control.
- **Post-selection inference:** conditions on lasso selection to form intervals for selected-model coefficients. Exact results use a fixed design and Gaussian errors with known variance. [Lee et al.](https://arxiv.org/abs/1311.6238) (2013/2016).

## Instancewise selection

- **Instancewise selection:** L2X learns a feature subset for each example to explain a fixed predictor; this differs from one global subset used for all observations. [Learning to Explain](https://proceedings.mlr.press/v80/chen18j.html) (ICML 2018).
- **[INVASE](https://openreview.net/forum?id=BJg_roAcK7)** — 2019. A selector, predictor and baseline network learn instance-specific feature subsets through actor–critic training; the selected variables and subset size can change between observations.

## Cost-sensitive and adaptive acquisition

- **Dynamic feature selection:** learns a policy approximating greedy conditional-mutual-information acquisition from observed inputs. Recovery of the greedy policy assumes optimal training; it is not a globally optimal acquisition guarantee. [Covert et al.](https://proceedings.mlr.press/v202/covert23a.html) (ICML 2023).

## Evaluation and comparative evidence

### Validation and selection stability

- **Selection leakage:** choosing features before resampling can bias estimated prediction error. [Ambroise and McLachlan](https://doi.org/10.1073/pnas.102102699) (2002) demonstrate the problem in microarray classification; [pipeline guidance](https://scikit-learn.org/stable/common_pitfalls.html#data-leakage) keeps selection inside training folds.
- **Search overfitting:** a noisy validation criterion can overfit selector, subset-size and predictor choices. Nested resampling or an untouched test set must evaluate the complete search, including learned preprocessing. [Cawley–Talbot](https://jmlr.org/papers/v11/cawley10a.html) (2010).
- **MUVR:** combines variable selection with repeated double cross-validation in multivariate modeling. [Shi et al.](https://academic.oup.com/bioinformatics/article/35/6/972/5085367) (2018/2019); [code](https://gitlab.com/CarlBrunius/MUVR).
- **Stability measurement:** compares scores, ranks, or subsets under data perturbations. [Kalousis, Prados, Hilario](https://cui.unige.ch/~kalousis/papers/stability/KalousisPradosHilarioKIS2007.pdf) (2007); [Nogueira, Sechidis, Brown](https://jmlr.org/papers/v18/17-514.html) (2018) provide a chance-corrected measure, intervals, and tests.

### Correlated features and importance bias

- **Forest importance bias:** Strobl et al. show preference for variables with more categories or different measurement scales in studied forest importance measures. [Paper](https://doi.org/10.1186/1471-2105-8-25) (2007). Importance is not an unbiased relevance test.
- **Conditional permutation importance:** permutes within a conditioning scheme to account for predictor dependence. [Strobl et al.](https://epub.ub.uni-muenchen.de/2821/1/deck.pdf) (2008); [Gregorutti et al.](https://arxiv.org/abs/1310.5726) (2013/2017) analyze correlation effects and recursive elimination.
- **Held-out permutation importance:** measures a fitted model's score loss after permuting a feature. Correlated substitutes can mask importance; the result depends on the model and score. [Definitions and limitations](https://scikit-learn.org/stable/modules/permutation_importance.html).

## Task-specific selection and method recommendation

- **Uplift modeling:** selects inputs for heterogeneous treatment-effect prediction rather than ordinary outcome prediction. [Zhao et al.](https://arxiv.org/abs/2005.03447) (2020) develop task-specific statistical and information-theoretic criteria.
- **Selector recommendation:** learns from dataset metafeatures and previous selector evaluations. [Wang et al.](https://arxiv.org/abs/1402.0570) (2014), [Parmezan et al.](https://doi.org/10.1016/j.eswa.2017.01.013) (2017), and [synthetic metatraining](https://arxiv.org/abs/2005.09856) (2020) study this AutoML connection.

## Software

- **Python — classical selection:** [scikit-learn](https://scikit-learn.org/stable/modules/feature_selection.html) provides filters, model thresholds, RFE/RFECV, and sequential selection; [scikit-feature](https://github.com/jundongl/scikit-feature) collects research implementations.
- **Python — learned selection and error control:** [Concrete autoencoders](https://github.com/mfbalin/Concrete-Autoencoders), [STG](https://github.com/runopti/stg), [LassoNet](https://github.com/lasso-net/lassonet), [knockpy](https://amspector100.github.io/knockpy/).
- **Supporting tools:** [feature-selector](https://github.com/WillKoehrsen/feature-selector) removes missingness/constant/collinearity-based columns; these are data-quality rules. [BoostARoota](https://github.com/chasedehan/BoostARoota) implements XGBoost-based shadow comparisons.
- **R — search and filters:** [FSinR](https://cran.r-project.org/package=FSinR) ([paper](https://arxiv.org/abs/2002.10330)) and [praznik](https://cran.r-project.org/package=praznik); [copent](https://cran.r-project.org/package=copent) ([paper](https://arxiv.org/abs/2005.14025)) supplies supporting copula/transfer-entropy estimation.
- **R — model-based selection:** [Boruta](https://cran.r-project.org/package=Boruta), [VSURF](https://cran.r-project.org/package=VSURF), [glmnet](https://cran.r-project.org/package=glmnet), [spikeSlabGAM](https://cran.r-project.org/package=spikeSlabGAM) ([paper](https://www.jstatsoft.org/article/view/v043i14)), [knockoff](https://cran.r-project.org/package=knockoff).
- **L0Learn:** approximate L0-regularized regression and classification through coordinate descent and local combinatorial search; C++ implementation with R/Python interfaces. [Package paper](https://jmlr.org/papers/v24/22-0189.html) (2023).
- **Archived software:** [fscaret](https://cran.r-project.org/package=fscaret) was archived by CRAN in August 2025; retained for historical reference.

## Surveys and further reading

- [An Introduction to Variable and Feature Selection](https://jmlr.org/papers/v3/guyon03a.html) (2003) — Guyon and Elisseeff. Relevance, redundancy, ranking, subset search, and validation.
- [A Survey on Feature Selection](https://doi.org/10.1016/j.procs.2016.07.111) (2016) — Miao and Niu. Filter, wrapper, and embedded approaches.
- [Feature Selection: A Data Perspective](https://arxiv.org/abs/1601.07996) (2016) — Li et al. Conventional, structured, heterogeneous, and streaming data.
- [Feature Selection and Feature Extraction in Pattern Analysis](https://arxiv.org/abs/1905.02845) (2019) — Ghojogh et al. Selection of existing variables and construction of new representations.
- **Attribution rankings:** [Man–Chan](https://arxiv.org/abs/2005.12483) (2020) compare permutation, LIME and SHAP rankings for random forests; reported stability differences do not establish predictive gains from selecting those features.

## Related topics

[Feature extraction](https://mlpapers.org/feature-extraction/) · [Interpretability](https://mlpapers.org/interpretability/) · [Causal inference](https://mlpapers.org/causal-inference/) · [Ensemble learning](https://mlpapers.org/ensemble-learning/) · [AutoML](https://mlpapers.org/automl/).

- **Representation learning:** ordinary autoencoders construct latent features. [Baldi](https://proceedings.mlr.press/v27/baldi12a.html) (2012); [Kingma and Welling](https://arxiv.org/abs/1906.02691) (2019). Concrete autoencoders instead constrain the encoder to select original inputs.
