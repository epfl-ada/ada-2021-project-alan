## Recreating the Political Spectrum with Quotebank
<i style="text-align: center;"> Ali Benabdallah, Cornelius van den Heuvel, Jiri Jirka Lhotka, Francesco Salvi</i>

### Abstract
The search for political spectrum, i.e. a set of independent political dimensions which enable characterization of political positions in relation to one another, has long been a focus of political science research. While most commonly used models are primarily based on the left/right division dating all the way from the French Revolution, many political scientists argue it no longer accurately characterizes the political divisions of today ([1](https://www.perlego.com/book/532600/beyond-liberal-and-conservative-reassessing-the-political-spectrum-pdf), [2](https://ideas.repec.org/p/osf/socarx/tr8g5.html)). In this project, we propose to create a political spectrum empirically by leveraging the Quotebank dataset ([3](https://dl.acm.org/doi/10.1145/3437963.3441760)). Using topic and sentiment extraction applied to recent quotes of American politicians on the federal level, we will obtain their sentiments on current issues and perform dimensionality reduction to find the most divisive axes. Further analysis and interpretation of the resulting vector space will allow us to redefine the political spectrum based on the most contentious issues.  


### Files in this repo

- **[DataWrangling.ipynb](DataWrangling.ipynb)**: Data preprocessing
- **[TopicExtraction.ipynb](TopicExtraction.ipynb)** and **[SentimentAnalysis.ipynb](SentimentAnalysis.ipynb)**: Initial explorations of tools for eponymous methods 


### Research questions

1. **What are the most important axes of political division today?**
To answer this question, we will first find the most significant dimensions of the topic-sentiment vector space (for technical details see the [Methods](#Methods) section). These dimensions define the topics on which current politicians are most divided. Then, to achieve interpretability, we will look at the topic-sentiment combinations that most define each axis's extremes. From this, we will empirically derive and interpret the most important axes similarly to how the Big Five personality traits were derived in psychology [(4)](https://dl.acm.org/doi/10.1145/3437963.3441760).

2. **What defines the Democrat-Republican political divide?**
Having found and interpreted the axes, we will further look at individual politicians' positions to answer the following questions: Where does the average democrat/republican stand? Are the parties equally divided or is one more clustered around its centre than the other? Are moderate politicians from each party closer to the other party's mean than radicals?

3. **Extension: Media bias**
As an extension of the project, we propose to also analyse the position of media within the topic-sentiment vector space. This would consist of grouping all quotes according to their source newspaper, extracting the topic and sentiment associated with each quote, and analysing which newspapers cluster together in the topic-sentiment vector space – indicating a biased news source – and which newspapers cover a wide spectrum of viewpoints. 

4. **Extension: Where do you stand?**
As another extension, we propose to turn the quotes which best describe the vector vector space (e.g. axes extremes) into a questionnaire where participants can express their agreement/disagreement with such statements and discover their position on our political map, similarly to what [politicalcompass.org](https://www.politicalcompass.org/) provides.

### Methods
Our pipeline can be split into a series of phases, each associated with certain tools/methods:

- **Data Wrangling**: Quotebank quotation-centric database will be processed for each year of phase E (2015-2020), to perform initial cleanings, filter for US modern politicians using Wikidata Qids and enrich data with domains information. This has already been largely accomplished while exploring data for Milestone 2. Tools: **Apache Sparks, Wikidata APIs**.

- **Topic Extraction**: The preprocessed data will then be used to perform topic extraction and get a list of meaningful topics, with a pretrained model based on BERT. Then, keeping only the quotes of politicians with a specified minimum number of quotes, each entry in the filtered dataset will be assigned a (list of) topic(s), discarding irrelevant quotes. Tools: **BERTopic, LDA**.

- **Sentiment Analysis**: Each quote of the dataset will be assigned a score based on the sentiment it conveys, ranging from negative, neutral to positive. Tools: **VADER, TextBlob**.

- **Building opinions, dimensionality reduction**: For each politician, we will define and calculate their **opinion** as a vector with dimensionality equal to the number of extracted topics where each value is the average of all the sentiments in quotes about the topic. Then, we will perform dimensionality reduction to extract the most meaningful axes. Tools: **PCA, t-SNE**.

### Feasibility assessment
- **Data Wrangling**: Already done. Loading and filtering the entire dataset yielded a *reduced dataset* of approximately 9% of original size - about 12 milions quotes.
- **Topic Extraction**: 5 hours to fit BERTopic and 4 hours to assign topic labels to the filtered dataset. 
- **Sentiment analysis**: About 1 hour to assign a sentiment to each quote in the filtered dataset.

### Proposed timeline
**November 12 - November 26**: Homework 2 + start Scaling up

**November 26 - December 3**: Scaling up: Topic Extraction and Sentiment Analysis on the whole dataset, building opinion vectors.

**December 3 - December 10**: Dimensionality, interpretation of the axes reduction and case studies (by party, newspaper, specific people...).

**December 10 - December 17**: Data story writeup, notebooks cleaning and answering research questions.

### Team organization
In principle, the whole team will contribute in all the steps of the pipeline, since we all wish to gain experience with them. Hoewever, to avoid [diffusion of responsibility](https://en.wikipedia.org/wiki/Diffusion_of_responsibility), we will designate specific people serving as "leaders" for specific tasks:
- Lukas – Sentiment Analysis
- Ali – Topic Extraction
- Jirka – Scale-up, Axes interpretation
- Francesco – Data Wrangling, case studies and Data Story


### Conclusion
In recent years, ML-based natural language processing has achieved impactful results in political science. For example, sentiment-analysis-based models have been shown to extract political ideology from news articles with 70% accuracy and F1-scores nearing 0.8 ([6](https://arxiv.org/abs/1809.03485), [7](https://aclanthology.org/P14-1105/)), showing that automated detection of political sentiments – the core of the method presented here – is possible and meaningful. In this project, we will leverage sentiment analysis together with Quotebank, a vast dataset of quotations, to (1) extract current topics that govern the political debate, and (2) find the most divisive topic-sentiment axes, recreating the political spectrum. Two main expected challenges of this work are: (1) missing values in the opinion vectors as not all politicians have expressed their opinion on all extracted topics; and (2) interpretation of the most significant axes of the political spectrum. We are confident that these issues are addressable and that our approach will lead to novel insights into the American politics of today.
