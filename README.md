# AG-Evaluation

AG is a method for reliable evaluation of distributional semantic models.  
It was introduced in the paper [Improving Reliability of Word Similarity Evaluation by Redesigning Annotation Task and Performance Measure](https://aclweb.org/anthology/W/W16/W16-2519.pdf). 

Here we provide:
- A python implementation of the method
- A suite of matching datasets in Hebrew (some of them were developed as part of the paper [The Interplay of Semantics and Morphology in Word Embedding](https://www.aclweb.org/anthology/E/E17/E17-2067.pdf))
- An example script using the method

### Requirements
- Python 2.7
- [gensim](https://radimrehurek.com/gensim/install.html) (only for the example script)

### Example
Run the following line on shell:
```sh
$ python sample.py
```
The code in *sample.py* loads a gensim word2vec model and runs evaluation on the 'nn' dataset.  
Notice the model it uses (*model.vec*) covers only part of the vocabulary, thus the output will contain messages of the type "could not get similarity..." for the OOV words in the datasets.

### Can I use a model created by other library (not gensim)?
Sure, the model does not have to be a gensim model.  
It just needs to be encapsulated in a class with a method "similarity" which takes two words and returns a score.

### Can I use the AG method to evaluate models of other languages?
Of course, you just need to provide matching datasets which follow the structure described in the paper.

### Can I perform more fine-grained analysis?
Yes, you can filter comparisions by different properties of the `Comparison` class (declared in *evaluator.py*).  
For example, by changing the lambda in the last line of *sample.py* from `comp: comp.set_name == 'nn'` to `comp: comp.set_name == 'nn' and comp.compare_type == 'randoms'`, you include only "positive-random" comparisons in the evaluation.

### The provided datasets
The 'datasets' directory is divided into several sub-directories: 
* "basic" - in these datasets, all the words are base forms
* "inflected" - these datasets contain the same words as 'basic', but inflected to other forms (to evaluate the effect of rich morphology)
* "rare" - in these datasets, all the target words are rare (occur less than 100 times in Hebrew wikipedia)
* "ambiguous" - in these datasets, the target words are morphologically ambiguous (to evaluate the ambiguity effect)
* "cohyponyms" - datasets in which the preferred-relation is defined as "cohyponyms" (in contrast to "hyponym-hypernym" in the other datasets)

### References
If you make use of this software for research purposes, we'll appreciate citing the following:

	@InProceedings{avraham-goldberg:2016:RepEval,
	  author    = {Avraham, Oded  and  Goldberg, Yoav},
	  title     = {Improving Reliability of Word Similarity Evaluation by Redesigning Annotation Task and Performance Measure},
	  booktitle = {Proceedings of the 1st Workshop on Evaluating Vector-Space Representations for NLP},
	  month     = {August},
	  year      = {2016},
	  address   = {Berlin, Germany},
	  publisher = {Association for Computational Linguistics},
	  pages     = {106--110},
	  url       = {http://anthology.aclweb.org/W16-2519}
	}

### Contact
For any question, please contact oavraham1@gmail.com
