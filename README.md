# NER Based Ranker
Contains the source code for CSC 583 project: "Ranking Search Engine Results Based on Named Entities in Queries".

Instructions for running the Lucene component of the code to generate Top-20 candidate answers for each Jeopardy question:
* The index must be pasted inside the `LucenePreprocessor/src/main/resources` folder. To generate it on the Jeopardy dataset, you must first download the dataset from [here](https://www.dropbox.com/s/nzlb96ejt3lhd7g/wiki-subset-20140602.tar.gz?dl=0) and extract it into into a folder called `wiki_dataset`. The index can then be built by running `IndexTrainer.java` inside `LucenePreprocessor/src/main/java/`.
* Run `QueryEngine.java` to create a `questions` folder which will contain sub-folders of the format Qi where i = [1,2..100], containing the titles of the top-20 most relevant documents for each question based on Lucene  `LMDirichletSimilarity`.

Instructions for finetuning NER, generating NER labels for jeopardy questions and candidates, EntityTFIDF implementation and evaluation:
* For loading the SSL NER models, and fine-tuning on the tweetner7 dataset, run the notebook titled `tweetner-dataset-preprocessing+fully-supervised-ner-example.ipynb`. This notebook also evaluates TFIDF and Lucene based on MRR.
* For loading the finetuned model, generating NER labels for every question in Jeopardy, as well as for each token in each of the 2000 documents (obtained after Lucene filtering), run the notebook titled `jeopardy_NER_tagging.ipynb`. This notebook also evaluates EntityTFIDF based on MRR.
