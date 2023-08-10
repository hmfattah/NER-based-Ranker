# NER Based Ranker
This project aims to incorporate Named Entity Recognition (NER) into ranking search engine results for a given query. The idea we propose is to first identify the Named Entities in the query. We then propose to modify the TF-IDF algorithm to incorporate keyword entity types: to rank the search results for a given query, we propose to define the term frequency of a term t in document d as the number of times that t occurs in d given that term t in document d has the same entity type as that in the query. Similarly, we propose to modify the definition of document frequency to incorporate entity types as well i.e., document frequency becomes the number of documents in the collection that the term occurs in, given that the term has the same entity type as that in the query.

We are interested in the problem of identifying Named Entities in web queries, which have the characteristic that they are very short and are usually typed in lowercase, so there is a lack of sufficient context, presenting a challenge for traditional NER approaches.

We use an NER algorithm based on a transformer that is trained in a semi-supervised fashion in conjunction with a series of statistical and linguistic heuristics. We train this NER algorithm first on the CoNLL-2003 dataset, and then fine-tune it on a dataset of tweets scrapped from Twitter, since it seems that datasets of tweets annotated with Named Entities are more readily available than datasets of web queries of the same form: tweets may be a good substitute for web queries.

We answer the research question: Does a modified TF-IDF ranking algorithm based on Named Entity types qualitatively improve the ranking of the search results compared to traditional TF-IDF? We still plan to use traditional TF-IDF as a fallback option, and as a baseline.

# Instructions
Instructions for running the Lucene component of the code to generate Top-20 candidate answers for each Jeopardy question:
* The index must be pasted inside the `LucenePreprocessor/src/main/resources` folder. To generate it on the Jeopardy dataset, you must first download the dataset from [here](https://www.dropbox.com/s/nzlb96ejt3lhd7g/wiki-subset-20140602.tar.gz?dl=0) and extract it into into a folder called `wiki_dataset`. The index can then be built by running `IndexTrainer.java` inside `LucenePreprocessor/src/main/java/`.
* Run `QueryEngine.java` to create a `questions` folder which will contain sub-folders of the format Qi where i = [1,2..100], containing the titles of the top-20 most relevant documents for each question based on Lucene  `LMDirichletSimilarity`.

Instructions for finetuning NER, generating NER labels for jeopardy questions and candidates, EntityTFIDF implementation and evaluation:
* For loading the SSL NER models, and fine-tuning on the tweetner7 dataset, run the notebook titled `tweetner-dataset-preprocessing+fully-supervised-ner-example.ipynb`. This notebook also evaluates TFIDF and Lucene based on MRR.
* For loading the finetuned model, generating NER labels for every question in Jeopardy, as well as for each token in each of the 2000 documents (obtained after Lucene filtering), run the notebook titled `jeopardy_NER_tagging.ipynb`. This notebook also evaluates EntityTFIDF based on MRR.
