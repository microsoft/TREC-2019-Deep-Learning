# TREC 2019 Deep Learning Track Guidlines

## Timetable

* May 24th:                Website goes live with data and guidelines
* May 28th:         Datasets released
* August 7:          Submissions close
* November 13-15:     TREC conference

## Introduction

The Deep Learning Track studies information retrieval in a *large training data* regime. This is the case where the number of training queries with at least one positive label is at least in the tens of thousands, if not hundreds of thousands or more. This corresponds to real-world scenarios such as training based on click logs and training based on labels from shallow pools (such as the pooling in the TREC Million Query Track or the evaluation of search engines based on early precision).

Our main goal is to study what methods work best in this regime. For example, do the same methods that work on small data also work on large data? How much do methods improve when given more training data? What external data and weak supervision can be brought in to bear in this scenario, and how useful is it to combine full supervision with other forms of supervision including transfer learning?

Certain machine learning based methods, such as methods based on deep learning are known to require very large datasets for training. Lack of such large scale datasets has been a limitation for developing such methods for common information retrieval tasks, such as document ranking.  One of the goals of the track is to make such large-scale datasets publicly available, which could enable the development of different machine learning architectures without being constrained by the amount of training data. Through the evaluation methodologies we release as part of the track, we also enable participants to compare the performance of their methods with other state of the art methods.

## Deep Learning Track Tasks

The deep learning track has two tasks: Passage ranking and document ranking. Both use a large human-generated set of training labels, from the MS-MARCO [http://msmarco.org](http://msmarco.org)] dataset.

The two tasks use the same 1000 test queries. They also use the same form of training data with usually one positive training document per training query. In the case of passage ranking, there is a direct human label that says the passage can be used to answer the query, whereas for training the document ranking task we transfer the same passage-level labels to document-level labels.

### Use of external information

You are allowed to use external information while developing your runs. When you submit your runs, please fill in a form listing what evidence you used, for example an external corpus such as Wikipedia or a pre-trained model (e.g. word embeddings).

When submitting runs, participants will be able to indicate what resources they used. This could include the provided set of document ranking training data, but also optionally other data such as the passage ranking task labels or external labels or pretrained models. This will allow us to analyze the runs and break they down into types.

IMPORTANT NOTE: It is prohibited to use evidence from the MS-MARCO Question Answering task in your submission. That dataset reveals some minor details of how the MS MARCO dataset was constructed that would not be available in a real-world search engine; hence, should be avoided.

### Dataset and document collection

Type	Filename	File size	Num Records	Format
Corpus	msmarco-docs.tsv	22 GB	          3,213,835 	tsv: docid, url, title, body
Corpus	msmarco-docs.trec	22 GB	          3,213,835 	TREC DOC format
Corpus	msmarco-docs-lookup.tsv	101 MB	          3,213,835 	tsv: docid, offset_trec, offset_tsv
Train	msmarco-doctrain-queries.tsv	15 MB	              367,013 	tsv: qid, query
Train	msmarco-doctrain-top100	1.8 GB	        36,701,116 	TREC submission: qid, "Q0", docid, rank, score, runstring
Train	msmarco-doctrain-qrels.tsv	7.6 MB	              384,597 	TREC qrels format


Passage 1) corpus 8.8 million, 2) 500k training queries and qrels
[Corpus of Passages](https://msmarco.blob.core.windows.net/msmarcoranking/collection.tar.gz)


Document 1) corpus 3.3 million
[Corpus of Documents](https://msmarco.blob.core.windows.net/msmarcoranking/fulldocs.tsv.gz)
[Queries](https://msmarco.blob.core.windows.net/msmarcoranking/queries.tar.gz)
[qrels](https://msmarco.blob.core.windows.net/msmarcoranking/qrels.train.tsv)
test set 1000 queries

### Passage ranking task
The first task focuses on passage ranking. We have two subtasks related to this: Full ranking and top-1000 re-ranking.

In context of full ranking subtask, given a question, you are expected to rank passages from the full collection in terms of their likelihood of containing an answer to the question. You can submit up to 1000 passages for this task.

In context of top-1000 re-ranking subtask, we will be providing you with an initial ranking of 1000 passages (with no particular order) and you are expected to re-rank these passages based on their likelihood of containing an answer to the question. 

### Document ranking task

Similar to the passage ranking task, the document ranking task also has a full ranking and re-ranking subtasks.

In the full ranking subtask, you are expected to rank documents based on their relevance to the question, where documents can be retrieved from the full document collection provided. You can submit up to 1000 documents for this task.

In the re-ranking subtask, we will be providing you with an initial ranking of 50 documents and you are expected to re-rank these documents in terms of their relevance to the question.

## Submission instructions

We will be following a similar format as the ones used by most TREC submissions, which is repeated below. White space is used to separate columns. The width of the columns in the format is not important, but it is important to have exactly six columns per line with at least one space between the columns.

```text
1 Q0 pid1    1 2.73 runid1
1 Q0 pid2    1 2.71 runid1
1 Q0 pid3    1 2.61 runid1
1 Q0 pid4    1 2.05 runid1
1 Q0 pid5    1 1.89 runid1
```
, where:

* the first column is the topic (query) number.
* the second column is currently unused and should always be "Q0".
* the third column is the official identifier of the retrieved passage in context of passage ranking task, and the identifier of the retrieved document in context of document ranking task. 
* the fourth column is the rank the passage/document is retrieved.
* the fifth column shows the score (integer or floating point) that generated the ranking. This score must be in descending (non-increasing) order.
* The sixth column is the ID of the run you are submitting.

## Evaluation and judging

We will be having two separate test sets: One test set contains 1000 queries with sparse labels directly reused from the MS-Marco dataset. The same 1000 queries will be used as the test set for both the passage retrieval and document retrieval tasks. More information regarding how these sparse labels were obtained can be found at https://arxiv.org/abs/1611.09268.

As the official evaluation set, we will be using a random subset of these 1000 queries containing 50 queries that are judged by NIST assessors. For this purpose, we will be using depth pooling and construct separate pools for the passage ranking and document ranking tasks. Passages/documents in these pools will then be labelled by NIST assessors using multi-graded judgments. 


## Coordinators

Nick Craswell (Microsoft), Bhaskar Mitra (Microsoft), Emine Yilmaz (UCL) and Daniel Campos (Microsoft)

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

# Terms and Conditions
The MS MARCO datasets are intended for non-commercial research purposes only to promote advancement in the field of artificial intelligence and related areas, and is made available free of charge without extending any license or other intellectual property rights. The dataset is provided “as is” without warranty and usage of the data has risks since we may not own the underlying rights in the documents. We are not be liable for any damages related to use of the dataset. Feedback is voluntarily given and can be used as we see fit. Upon violation of any of these terms, your rights to use the dataset will end automatically.

# Legal Notices

Microsoft and any contributors grant you a license to the Microsoft documentation and other content
in this repository under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/legalcode),
see the [LICENSE](LICENSE) file, and grant you a license to any code in the repository under the [MIT License](https://opensource.org/licenses/MIT), see the
[LICENSE-CODE](LICENSE-CODE) file.

Microsoft, Windows, Microsoft Azure and/or other Microsoft products and services referenced in the documentation
may be either trademarks or registered trademarks of Microsoft in the United States and/or other countries.
The licenses for this project do not grant you rights to use any Microsoft names, logos, or trademarks.
Microsoft's general trademark guidelines can be found at http://go.microsoft.com/fwlink/?LinkID=254653.

Privacy information can be found at https://privacy.microsoft.com/en-us/

Microsoft and any contributors reserve all other rights, whether under their respective copyrights, patents,
or trademarks, whether by implication, estoppel or otherwise.
