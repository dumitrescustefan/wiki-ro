# Wiki-ro

This corpus is a thoroughly cleaned dump of the June 2020 Romanian Wikipedia. It is meant as a reference text upon which to calculate Language Model capacity and/or perplexity. 

### Format

The corpus is split in three files:

* ``wiki.txt.train``: 2.1 M lines, 44 M words, 285 MB
* ``wiki.txt.valid``: 14 K lines, 276 K words, 1.8 MB
* ``wiki.txt.test``: 16 K lines, 327 K words, 2.2 MB

The text files are articles, sentence-segmented; articles are delimited by an empty line. The corpus contains only the text of articles, not their titles, as the target is to have complete, fully-formed sentences. 

The splits contain only full articles. They do not contain _all_ the articles in the June 2020 dump, as many articles were dropped due to being stubs, containing only lists, foreign words/sentences, too many numbers, etc.  

### How to get

Due to GitHub's maximum file limit, we had to zip and split the files. Thus, in the ``corpus`` folder there are three archive parts. To obtain the raw text corpus files, concatenate and unzip:

```shell
cat wiki-ro-split-* > wiki-ro.zip
unzip wiki-ro.zip
```

### Evaluation 

At this moment, we have performed a zero-shot evaluation of a transformer-based [masked language model](https://huggingface.co/dumitrescustefan/bert-base-romanian-cased-v1).

For MLM language models, we calculate the pseudo-log-likelihood scores (PLLs) as defined [here](https://arxiv.org/abs/1910.14659). Running ``mlm score --gpus 0 --split-size 64 --max-utts 1000000 --model dumitrescustefan/bert-base-romanian-cased-v1 --mode ref wiki.txt.test > out.txt`` [source](https://github.com/awslabs/mlm-scoring): 

On ``wiki.txt.valid``:
```
Token-level (P)PPL: 9.8506
Word-normalized (P)PPL: 29.0897
```

On ``wiki.txt.test``:
```
Token-level (P)PPL: 9.6546
Word-normalized (P)PPL: 28.0043
```

### Citation 

_(Coming soon)_



