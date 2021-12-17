# A data-driven Political Compass

*Francesco Salvi, Jirka Lhotka, Lukas Cornelius van den Heuvel and Ali Benabdallah*

## Abstract

The search for political spectrum, i.e. a set of independent political dimensions which enable characterization of political positions in relation to one another, has long been a focus of political science research. While most commonly used models are primarily based on the left/right division dating all the way from the French Revolution, many political scientists argue it no longer accurately characterizes the political divisions of today ([1](https://www.perlego.com/book/532600/beyond-liberal-and-conservative-reassessing-the-political-spectrum-pdf), [2](https://ideas.repec.org/p/osf/socarx/tr8g5.html)). In this project, we propose to create a political spectrum empirically by leveraging the Quotebank dataset ([3](https://dl.acm.org/doi/10.1145/3437963.3441760)). Using topic and sentiment extraction applied to recent quotes of American politicians on the federal level, we will obtain their sentiments on current issues and perform dimensionality reduction to find the most divisive axes. Further analysis and interpretation of the resulting vector space will allow us to redefine the political spectrum based on the most contentious issues.  

## Repo structure

```bash
.
├── 1_DataWrangling.ipynb: Data wrangling, filtering and data enrichment.
├── 2_TopicExtraction.ipynb: Topic extraction and prediction.
├── 3_SentimentAnalysis.ipynb: Sentiment analysis.
├── 4_BuildOpinions.ipynb: Creation of the opinions matrix.
├── 5_TopicAnalysis.ipynb: Analyses of dominant and most divisive topics.
├── 6_PoliticalCompass.ipynb
├── Milestone2
│   ├── README_Milestone2.md
│   ├── SentimentAnalysis_exploration.ipynb
│   └── TopicExtraction_exploration.ipynb
└── README.md
```

## Research questions

1. **What are the most important axes of political division today?**
To answer this question, we will first find the most significant dimensions of the topic-sentiment vector space (for technical details see the [Methods](#Methods) section). These dimensions define the topics on which current politicians are most divided. Then, to achieve interpretability, we will look at the topic-sentiment combinations that most define each axis's extremes. From this, we will empirically derive and interpret the most important axes similarly to how the Big Five personality traits were derived in psychology [(4)](https://dl.acm.org/doi/10.1145/3437963.3441760).

2. **What defines the Democrat-Republican political divide?**
Having found and interpreted the axes, we will further look at individual politicians' positions to answer the following questions: Where does the average democrat/republican stand? Are the parties equally divided or is one more clustered around its centre than the other? Are moderate politicians from each party closer to the other party's mean than radicals?

## Methods
Our pipeline can be split into a series of phases, each associated with certain tools/methods:

- **Data Wrangling**: Quotebank quotation-centric database was processed for each year of phase E (2015-2020), to perform initial cleanings, filter for US modern politicians using Wikidata Qids and enrich data with domains information. This had already been largely accomplished while exploring data for Milestone 2. Tools: **Apache Sparks, Wikidata APIs**.

- **Topic Extraction**: The preprocessed data was then be used to perform topic extraction and get a list of meaningful topics, with a pretrained model based on BERT. Then, each entry in the filtered dataset was be assigned a (list of) topic(s), discarding irrelevant quotes. Tools: **BERTopic**.

- **Sentiment Analysis**: Each quote of the dataset was be assigned a score based on the sentiment it conveys, ranging from negative, neutral to positive. Tools: **VADER**.

- **Building opinions, dimensionality reduction**: For each politician, we have defined and calculated their **opinion** as a vector with dimensionality equal to the number of extracted topics where each value is the average of all the sentiments in quotes about the topic. Then, we have perform dimensionality reduction to extract the most meaningful axes. Tools: **PCA, t-SNE, UMAP, NCA**.

## Team contibution
In principle, the whole team contributed in all the steps of the pipeline, as we all wished to gain experience with them. Hoewever, to avoid [diffusion of responsibility](https://en.wikipedia.org/wiki/Diffusion_of_responsibility), we designated specific people serving as "leaders" for specific tasks:
- Francesco - Data Wrangling, Dimensionality Reduction, Notebooks Finalization
- Lukas - Sentiment Analysis, Topic Analysis, Data Story Visualizations
- Jirka - Scaling up, Building Opinions, Data Story Writeup
- Ali - Topic Extraction, Exploratory Analyses


## Conclusions
We have managed to find and interpret 3 axes that divide american politicians in accordance with their real-life beliefs (e.g. parties are divided, radicals further apart, moderates closer together), and have analyzed what are the most significant topics with respect to partisan divide. You can find out more about our work in this repository, or reading our [data story](https://the-political-compass.github.io/data-driven-political-compass/) as well as its [code](https://github.com/the-political-compass/data-driven-political-compass).
