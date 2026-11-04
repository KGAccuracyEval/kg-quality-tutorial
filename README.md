# Knowledge Graphs Data Quality at Scale: Challenges, Solutions, and Applications

Half-day tutorial (3 hours) at **CIKM 2026**, Rome, Italy.

**Presenters**

- [Stefano Marchesin](https://www.dei.unipd.it/~marches1/), University of Padua, Italy
- [Gianmaria Silvello](https://www.dei.unipd.it/~silvello/), University of Padua, Italy
- Omar Alonso, Amazon, USA

## Abstract

Knowledge Graphs (KGs) are foundational infrastructure for search, question answering, and entity-centric applications, on the open web and within domain-specific platforms. Their lifecycle, from construction over heterogeneous sources to evaluation at scale and use in downstream tasks, raises a coupled set of data management problems that shape the reliability and utility of every system built on top of them. This tutorial offers a high-level view of KG data quality at scale, organized along the three stages of the lifecycle. We first frame KG construction and the open challenges that arise when facts are extracted from noisy, evolving sources. We then turn to evaluation, covering efficient quality estimation, as well as the role of Large Language Models (LLMs) as validators and auxiliary signals. We close with downstream applications, including entity-oriented search and scalable defect detection, which translate evaluation outcomes into operational decisions.

## Tutorial Slides

- [Tutorial slides (PDF)](cikm2026-tutorial-kg-data-quality.pdf)

## Prerequisites

Basic structure of RDF KGs (triples, predicates, entities) and elementary probability and statistics (expectation, variance, confidence intervals). No prior knowledge of survey sampling theory, Bayesian inference, or LLM internals is required.

## Outline

The tutorial follows the three stages of the KG lifecycle: construction, evaluation, and downstream use. Evaluation outcomes feed back into curation and re-estimation.

### Part 1. KG Construction and Data Quality Challenges

**1.1 Constructing KGs at scale.** CORE as a worked example of KG construction under limited annotation budgets: distant supervision, relation extraction, and three workflows (bootstrapping, deployment, active learning). Where quality issues enter a construction pipeline, and lessons from industrial KGs.

**1.2 Data quality challenges of evolving KGs.** Quality dimensions and the scope of the tutorial (accuracy). Why structural checks such as SHACL constraints are necessary but not sufficient. Where errors sit in a real KG, the cost structure of manual verification, ad hoc sampling in current practice, and the trade-offs of automated validation.

### Part 2. Evaluation Methodologies

**2.1 Sampling-based accuracy estimation.** KG accuracy estimation as constrained minimization of annotation cost. The cluster-based cost model of Gao et al. (PVLDB 2019). Simple random sampling, two-stage weighted cluster sampling (TWCS), and stratified TWCS.

**2.2 From Wald to Wilson to credible intervals.** Coverage failures of the Wald interval in the high-accuracy, small-sample regime of KG evaluation. The Wilson interval for cluster and stratified designs. Bayesian credible intervals, equal-tailed versus HPD intervals, prior choice, and the adaptive HPD (aHPD) procedure.

**2.3 Utility-oriented and budget-aware estimation.** Utility of facts derived from SPARQL query logs, stratification by utility, and budget allocation across strata. Case study on DBpedia; heavy-tailed utility and cold start.

**2.4 LLMs for KG quality assessment.** LLMs as direct validators: the FactCheck benchmark (internal knowledge, retrieval augmentation, multi-model consensus) and what to test before trusting an LLM validator. LLMs as stratification signals: aggregation of LLM judgments into strata and distillation to scale the signal.

### Part 3. Downstream Applications and Open Problems

**3.1 Veracity-driven entity search.** Entity cards and dynamic entity summarization. Relevance and veracity as two axes of evaluation. Veracity at the entity level in entity ranking (eRank) and at the fact level in defect detection (ALADDIN).

**3.2 Open problems.** Evolving KGs (requirements, challenges, temporal dynamics); transfer of signals and models across KGs; soft-label annotation; KG accuracy for LLM-based applications.

## Papers presented in the tutorial

| Venue | Paper | Tutorial | Link |
|---|---|---|---|
| Database 2023 | S. Marchesin et al. Building a Large Gene Expression-Cancer Knowledge Base with Limited Human Annotations | 1.1 | [doi:10.1093/database/baad061](https://doi.org/10.1093/database/baad061) |
| PVLDB 2024 | S. Marchesin and G. Silvello. Efficient and Reliable Estimation of Knowledge Graph Accuracy | 2.1, 2.2 | [doi:10.14778/3665844.3665865](https://doi.org/10.14778/3665844.3665865) |
| HCOMP 2024 | S. Marchesin, G. Silvello, and O. Alonso. Utility-Oriented Knowledge Graph Accuracy Estimation with Limited Annotations: A Case Study on DBpedia | 1.2, 2.3 | [AAAI OJS](https://ojs.aaai.org/index.php/HCOMP/article/view/31605) |
| CIKM 2024 | S. Marchesin, G. Silvello, and O. Alonso. Veracity Estimation for Entity-Oriented Search with Knowledge Graphs | 3.1 | [doi:10.1145/3627673.3679561](https://doi.org/10.1145/3627673.3679561) |
| SIGMOD 2025 | S. Marchesin and G. Silvello. Credible Intervals for Knowledge Graph Accuracy Estimation. Proc. ACM Manag. Data | 2.2 | [doi:10.1145/3725279](https://doi.org/10.1145/3725279) |
| CIKM 2025 | O. Irrera et al. Scaling Trust: Veracity-Driven Defect Detection in Entity Search | 3.1 | [doi:10.1145/3746252.3761208](https://doi.org/10.1145/3746252.3761208) |
| EDBT 2026 | F. Shami, S. Marchesin, and G. Silvello. Benchmarking Large Language Models for Knowledge Graph Validation | 2.4 | [doi:10.48786/edbt.2026.45](https://doi.org/10.48786/edbt.2026.45) |
| PVLDB 2026 | S. Marchesin, M. Ceccarello, and G. Silvello. LLMs as Stratification Signals for KG Accuracy Evaluation | 2.4 | [PDF](https://www.dei.unipd.it/~marches1/papers/mcs-vldb-2026.pdf) |
| ACM JDIQ 2026 | S. Marchesin et al. Cost-Effective Quality Evaluation for Evolving Knowledge Graphs | 1.2, 3.2 | [PDF](https://www.dei.unipd.it/~marches1/papers/msa-jdiq-2026.pdf) |

## Code and data

| Resource | Content | Link |
|---|---|---|
| KG accuracy estimation | Sampling designs (TWCS, stratified TWCS), Wilson and aHPD intervals; DBpedia utility study with annotated subsets and SPARQL utility logs; eRank and ALADDIN pipelines | [github.com/KGAccuracyEval](https://github.com/KGAccuracyEval) |
| LLM stratification | Code for PVLDB 2026 | [github.com/kg-quality/llm4kg-accuracy](https://github.com/kg-quality/llm4kg-accuracy) |
| FactCheck | Benchmark and RAG corpus for LLM-based KG validation (EDBT 2026) | [github.com/FactCheck-AI](https://github.com/FactCheck-AI) |
| CORE | Gene expression-cancer KB and SPARQL endpoint; construction code | [zenodo.org/record/7577127](https://zenodo.org/record/7577127) · [github.com/GDAMining/core](https://github.com/GDAMining/core) |

## Datasets and collections

### Benchmarks for KG accuracy evaluation

| Dataset | Facts | Entity clusters | Accuracy μ | Labels | Papers | Tutorial |
|---|---:|---:|---|---|---|---|
| YAGO | 1,386 | 822 | 0.99 | crowd | PVLDB 2019, 2024 · SIGMOD 2025 · EDBT 2026 | 2.1, 2.2, 2.4 |
| NELL | 1,860 | 817 | 0.91 | crowd | PVLDB 2019, 2024, 2026 · SIGMOD 2025 | 2.1, 2.2, 2.4 |
| DBpedia 2015-10 | 9,344 | 2,936 | 0.85 | crowd + expert QC | HCOMP 2024 · SIGMOD 2025 · EDBT 2026 · PVLDB 2026 · CIKM 2025 | 1.2, 2.2–2.4, 3.1 |
| FactBench | 2,800 / 4,219 | 1,157 | 0.54 / 0.28 | synthetic errors | SIGMOD 2025, EDBT 2026 / PVLDB 2026 | 2.2, 2.4 |
| DisGeNET | 2,999,087 | 21,243 | 0.76 (CEM) · 0.9 / 0.5 / 0.1 (TEM) | synthetic | PVLDB 2024 | 2.2 |
| SYN 100M | 101,415,011 | 5,000,000 | 0.9 / 0.5 / 0.1 | synthetic | PVLDB 2024 · SIGMOD 2025 | not shown |
| YAGO-HQ / MQ / LQ | 20,433,311 | 4.2–4.4M | 0.75 / 0.50 / 0.25 | synthetic errors | PVLDB 2026 | 2.4 |

PVLDB 2019 refers to Gao et al., who also use MOVIE, a KG built at Amazon that is not public. DisGeNET and SYN 100M carry synthetic labels whose accuracy is set by the label model: CEM is the cluster error model, TEM the triple error model with error rates 0.1, 0.5, and 0.9. FactBench values refer to the two versions used in the papers listed before and after the slash.

Sources: YAGO and NELL samples from Ojha and Talukdar (KGEval, EMNLP 2017); DBpedia sample from Marchesin et al. (HCOMP 2024); FactBench from Gerber et al. (DeFacto, J. Web Semant. 2015); DisGeNET from Piñero et al. (Nucleic Acids Res. 2020); YAGO 4.5 from Suchanek et al. (SIGIR 2024).

### Construction and downstream collections

| Collection | Task | Size | Papers | Tutorial |
|---|---|---|---|---|
| CORE knowledge base | KG construction from the literature (gene expression and cancer) | 153,016 facts (KG3) | Database 2023 | 1.1 |
| DBpedia utility study | Utility-oriented accuracy estimation; utility from LSQ 2.0 SPARQL logs | 37,546 labels on 11,296 facts | HCOMP 2024 | 1.2, 2.3 |
| FactCheck RAG corpus | LLM fact validation with retrieved web evidence | 2,090,305 documents for 13,530 triples | EDBT 2026 | 2.4 |
| DBpedia-Entity v2 | Entity retrieval: ranking entities for a query (eRank) | 485 queries, 4.6M entities, runs of 12 systems | CIKM 2025 | 3.1 |
| DBpedia-Fact | Entity summarization: ranking an entity's facts for its card | 100 query–entity pairs, 4,069 facts | CIKM 2024, 2025 | 3.1 |
| DBpedia-Defect | Fact-level defect detection: training and testing ALADDIN | Utility-study facts; 1,000 held out for test | CIKM 2025 | 3.1 |

Sources: DBpedia-Entity v2 from Hasibi et al. (SIGIR 2017); DBpedia-Fact from Hasibi, Balog, and Bratsberg (Dynamic Factual Summaries for Entity Cards, SIGIR 2017); query logs from Stadler et al. (LSQ 2.0, Semantic Web 2024). All Part 3 collections are built on DBpedia 2015-10.

## Annotated reading list

Grouped by the part of the tutorial where each work is mainly discussed; alphabetical by first author within each part.

### Part 1. KG Construction and Data Quality Challenges

- S. Auer et al. DBpedia: A Nucleus for a Web of Open Data. ISWC 2007.
- A. Bonifati et al. Querying Graphs. Morgan & Claypool 2018.
- O. Deshpande et al. Building, maintaining, and using knowledge bases: a report from the trenches. SIGMOD 2013.
  Experience report on an industrial KB pipeline, from construction to use.
- J. Devlin et al. BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding. NAACL-HLT 2019.
- D. Esteves et al. Toward Veracity Assessment in RDF Knowledge Bases: An Exploratory Analysis. ACM J. Data Inf. Qual. 2018.
- W. Fan. Data Quality: From Theory to Practice. SIGMOD Rec. 2015.
- A. Hogan et al. Knowledge Graphs. Morgan & Claypool 2021.
  Reference text on KG data models, construction, quality, and refinement.
- L. Huang et al. A Survey on Hallucination in Large Language Models: Principles, Taxonomy, Challenges, and Open Questions. ACM Trans. Inf. Syst. 2025.
- I. F. Ilyas et al. Growing and Serving Large Open-domain Knowledge Graphs. SIGMOD Companion 2023.
- I. F. Ilyas et al. Saga: A Platform for Continuous Construction and Serving of Knowledge at Scale. SIGMOD 2022.
  Industrial platform for continuous KG construction and serving.
- P. D. Karp. How much does curation cost? Database 2016.
  Cost of manual curation in biological databases; context for the cost structure in 1.2.
- S. Marchesin et al. Building a Large Gene Expression-Cancer Knowledge Base with Limited Human Annotations. Database 2023.
  CORE: distant supervision and active learning to build a domain KB with a small expert annotation budget.
- S. Marchesin et al. Cost-Effective Quality Evaluation for Evolving Knowledge Graphs. ACM J. Data Inf. Qual. 2026.
  Requirements and open challenges for the quality evaluation of evolving KGs.
- N. F. Noy et al. Industry-scale Knowledge Graphs: Lessons and Challenges. Commun. ACM 2019.
  Lessons from KGs built and maintained at five companies.
- H. Paulheim. How much is a Triple? Estimating the Cost of Knowledge Graph Creation. ISWC Posters & Demonstrations 2018.
  Per-triple cost estimates for manually and automatically created KGs.
- H. Paulheim. Knowledge Graph Refinement: A Survey of Approaches and Evaluation Methods. Semantic Web 2017.
  Survey of KG completion and error detection, with a critique of their evaluation.
- A. Polleres et al. How Does Knowledge Evolve in Open Knowledge Graphs? TGDK 2023.
  Change in open KGs and its consequences for their management.
- J. Pujara, E. Augustine, and L. Getoor. Sparsity and Noise: Where Knowledge Graph Embeddings Fall Short. EMNLP 2017.
- Y. Qi et al. Evaluating Knowledge Graph Accuracy Powered by Optimized Human-Machine Collaboration. KDD 2022.
- R. Reinanda, E. Meij, and M. de Rijke. Knowledge Graphs: An Information Retrieval Perspective. Found. Trends Inf. Retr. 2020.
- K. Sun et al. Head-to-Tail: How Knowledgeable are Large Language Models (LLMs)? A.K.A. Will LLMs Replace Knowledge Graphs? NAACL 2024.
  Factual knowledge of LLMs on head, torso, and tail entities.
- D. Vrandečić and M. Krötzsch. Wikidata: a free collaborative knowledgebase. Commun. ACM 2014.
- R. Y. Wang and D. M. Strong. Beyond Accuracy: What Data Quality Means to Data Consumers. J. Manag. Inf. Syst. 1996.
  Consumer-oriented framework of data quality dimensions.
- G. Weikum et al. Machine Knowledge: Creation and Curation of Comprehensive Knowledge Bases. Found. Trends Databases 2021.
  Survey of KB creation and curation.
- A. Zaveri et al. Quality assessment for Linked Data: A Survey. Semantic Web 2016.
  Quality dimensions and metrics for Linked Data.

### Part 2. Evaluation Methodologies

- G. E. P. Box and G. C. Tiao. Bayesian Inference in Statistical Analysis. Wiley 2011.
- L. D. Brown, T. T. Cai, and A. DasGupta. Interval Estimation for a Binomial Proportion. Statistical Science 2001.
  Shows the erratic coverage of the Wald interval and compares alternatives, including Wilson and Jeffreys.
- W. G. Cochran. Sampling Techniques, 3rd Edition. Wiley 1977.
  Reference text on survey sampling: cluster, stratified, and multi-stage designs.
- T. Dalenius and J. L. Hodges. Minimum Variance Stratification. J. Amer. Statist. Assoc. 1959.
  The cumulative square-root-frequency rule for stratum boundaries.
- D. Dosso, S. B. Davidson, and G. Silvello. Credit Distribution in Relational Scientific Databases. Information Systems 2022.
  Lineage-based credit distribution; the basis for counting the facts that contribute to a query answer in 2.3.
- P. S. Efraimidis and P. G. Spirakis. Weighted Random Sampling with a Reservoir. Inf. Process. Lett. 2006.
- J. Gao et al. Efficient Knowledge Graph Accuracy Evaluation. PVLDB 2019.
  Cluster-based annotation cost model, TWCS, stratified and incremental evaluation; the starting point of Part 2.
- D. Gerber et al. DeFacto: Temporal and Multilingual Deep Fact Validation. J. Web Semant. 2015.
  Fact validation from web evidence; source of the FactBench dataset.
- M. H. Hansen and W. N. Hurwitz. On the Theory of Sampling from Finite Populations. Ann. Math. Statist. 1943.
- G. E. Hinton, O. Vinyals, and J. Dean. Distilling the Knowledge in a Neural Network. CoRR abs/1503.02531, 2015.
- R. Hoekstra et al. Robust Misinterpretation of Confidence Intervals. Psychon. Bull. Rev. 2014.
  Empirical evidence that researchers misread confidence intervals as post-data probability statements.
- H. Jeffreys. An Invariant Form for the Prior Probability in Estimation Problems. Proc. R. Soc. A 1946.
- J. Kerman. Neutral Noninformative and Informative Conjugate Beta and Gamma Prior Distributions. Electron. J. Stat. 2011.
- L. Kish. Methods for Design Effects. J. Off. Stat. 1995.
- L. Kish. Survey Sampling. Wiley 1965.
- D. Kraft. A Software Package for Sequential Quadratic Programming. DLR German Aerospace Center, Institute for Flight Mechanics, 1988.
- ★ S. Marchesin and G. Silvello. Credible Intervals for Knowledge Graph Accuracy Estimation. Proc. ACM Manag. Data (SIGMOD) 2025.
  Bayesian HPD credible intervals and the adaptive aHPD procedure.
- S. Marchesin and G. Silvello. Efficient and Reliable Estimation of Knowledge Graph Accuracy. PVLDB 2024.
  Wilson intervals for cluster and stratified designs; replaces the Wald interval in KG accuracy estimation.
- S. Marchesin, G. Silvello, and O. Alonso. Utility-Oriented Knowledge Graph Accuracy Estimation with Limited Annotations: A Case Study on DBpedia. HCOMP 2024.
  Utility of facts from SPARQL query logs and utility-based stratification on DBpedia.
- S. Marchesin, M. Ceccarello, and G. Silvello. LLMs as Stratification Signals for KG Accuracy Evaluation. PVLDB 2026.
  Aggregated LLM judgments as stratification signals, distilled to scale to large KGs.
- R. D. Morey et al. The Fallacy of Placing Confidence in Confidence Intervals. Psychon. Bull. Rev. 2016.
- P. Ojha and P. Talukdar. KGEval: Accuracy Estimation of Automatically Constructed Knowledge Graphs. EMNLP 2017.
  Source of the YAGO and NELL samples used in Part 2.
- F. Petroni et al. Language Models as Knowledge Bases? EMNLP-IJCNLP 2019.
- J. Piñero et al. The DisGeNET knowledge platform for disease genomics: 2019 update. Nucleic Acids Res. 2020.
- F. Shami, S. Marchesin, and G. Silvello. Benchmarking Large Language Models for Knowledge Graph Validation. EDBT 2026.
  FactCheck: LLMs as fact validators with internal knowledge, retrieval augmentation, and multi-model consensus.
- C. Stadler et al. LSQ 2.0: A Linked Dataset of SPARQL Query Logs. Semantic Web 2024.
  SPARQL query logs used to derive the utility of DBpedia facts in 2.3.
- F. M. Suchanek et al. YAGO 4.5: A Large and Clean Knowledge Base with a Rich Taxonomy. SIGIR 2024.
- J. S. Vitter. Random Sampling with a Reservoir. ACM Trans. Math. Softw. 1985.
- E. B. Wilson. Probable Inference, the Law of Succession, and Statistical Inference. J. Amer. Statist. Assoc. 1927.
  The score interval for a binomial proportion.
- X. Xu et al. A Survey on Knowledge Distillation of Large Language Models. CoRR abs/2402.13116, 2024.
- M. Zhang et al. Knowledge Graph Accuracy Evaluation: An LLM-Enhanced Embedding Approach. Int. J. Data Sci. Anal. 2024.
- L. Zheng et al. Crowdsourced Fact Validation for Knowledge Bases. ICDE 2022.

### Part 3. Downstream Applications and Open Problems

- K. Balog. Entity-Oriented Search. Springer 2018.
  Reference text on entity retrieval, entity cards, and the use of KGs in search.
- A. Bordes et al. Translating Embeddings for Modeling Multi-relational Data. NeurIPS 2013.
  TransE; the offline regressor of ALADDIN works on TransE-embedded facts.
- S. Denney and M. DiGiuseppe. Jev versus LLMs: Accuracy, Cost and Calibration on Seven Political Science Replications. arXiv:2610.06625, 2026. Preprint.
- X. L. Dong et al. Knowledge-Based Trust: Estimating the Trustworthiness of Web Sources. PVLDB 2015.
  Estimates source trustworthiness from the correctness of the facts a source provides.
- X. L. Dong, L. Berti-Équille, and D. Srivastava. Integrating Conflicting Data: The Role of Source Dependence. PVLDB 2009.
- F. Hasibi et al. DBpedia-Entity v2: A Test Collection for Entity Search. SIGIR 2017.
  Test collection for entity retrieval over DBpedia.
- F. Hasibi, K. Balog, and S. E. Bratsberg. Dynamic Factual Summaries for Entity Cards. SIGIR 2017.
  Query-dependent fact ranking for entity cards; source of the DBpedia-Fact collection.
- N. Q. V. Hung et al. An Evaluation of Aggregation Techniques in Crowdsourcing. WISE 2013.
- O. Irrera et al. Scaling Trust: Veracity-Driven Defect Detection in Entity Search. CIKM 2025.
  eRank for entity-level veracity in ranking and ALADDIN for fact-level defect detection with active learning.
- Y. Li et al. A Survey on Truth Discovery. SIGKDD Explor. 2015.
- ★ S. Marchesin, G. Silvello, and O. Alonso. Veracity Estimation for Entity-Oriented Search with Knowledge Graphs. CIKM 2024.
  Veracity as an evaluation axis orthogonal to relevance in entity summarization.
- S. Mohammed et al. The Five Facets of Data Quality Assessment. SIGMOD Rec. 2025.
- Vals AI. Independent Evaluation of Jev. Blog post, 2026.
- J. Wei et al. Long-form factuality in large language models. NeurIPS 2024.
- B. Xue and L. Zou. Knowledge Graph Quality Management: A Comprehensive Survey. IEEE Trans. Knowl. Data Eng. 2023.
- J. Zhang, X. Wu, and V. S. Sheng. Learning from crowdsourced labeled data: a survey. Artif. Intell. Rev. 2016.

## Acknowledgments

This work is supported by the HEREDITARY project ([hereditary-project.eu](https://hereditary-project.eu/)).
