Information Extraction
======================

Set Expansion
-------------

* Richard C. Wang. Language-Independent Class Instance Extraction Using the Web. Ph.D. Thesis 2009. http://www.cs.cmu.edu/~rcwang/papers/phd-thesis.pdf
    - Bilingual SEAL: Iteratively run two instances of iSEAL alternating source/target languages, checking if the new seed's translation exists in the other language set
    - Named entity translation: find frequently co-occurring chunks in the search engine snippet in the target language, ranked by snippet/excerpt frequency and inverse distance.
    - Relational SEAL: seed = pairs, wrappers = (left, middle, right), with a "reverse" flag, can be used for translation pair extraction, ~80% mean average precision


Multilingual NER
----------------

* Alexander E. Richman and Patrick Schone. Mining Wiki Resources for Multilingual Named Entity Recognition, ACL 2008. http://www.mt-archive.info/ACL-2008-Richman.pdf
    - Use categories to classifiy English pages, and map NE types via interwiki links. Use this as the type of a wikilink (intra-language link to another article). Foreign language knowledge is not requried.
    - If a foreign page doesn't have a link to its English translation, use cateogory translation to classify types
    - Trained a NER system (PhoenixIDF), tested on ACE 2007 (newswire) and Wikipedia held-out data, with approx. 0.82 ~ 0.84 F-value in Spanish, French, and other languages

* Sungchul Kim, Kristina Toutanova, and Hwanjo Yu. Multilingual Named Entity Recognition using Parallel Data and Metadata, ACL 2012. http://www.newdesign.aclweb.org/anthology-new/P/P12/P12-1073.pdf
    - Wiki-tagger: Built local and global taggers based on article categorization (as in Richman and Schone 2008)
    - Mapping-based taggger: a ranking (log-linear) model from English entities to foreign entity spans (Feng et al. 2004), trained on 100 parallel sentences with NEs and alignments
    - Combination of these two via semi-Markov CRF (Sarawagi, Cohen 2005) outperforms individual models (~91% F-value in Korean and Bulgarian)

Unsupervised NER
----------------

* Oren Etzioni et al. Unsupervised named-entity extraction from the web: An experimental study. Artificial Intelligence, 2005. http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.124.8829&rep=rep1&type=pdf
    - Extraction of unary and binary relation using Hearst-style lexico-syntactic patterns (LSPs; e.g., NP1 such as NPList2) generated from class names. Then validation by PMI co-occurence on the Web.
    - Recall improvement: Learning patterns from seeds and use them as discriminators, subclass extraction (chemists or bilologists as opposed to scientists) again by LSPs, and list extractor (exactly as in SEAL)
    - list extractor's extraction rate was the greatest (more than x40 increase)


* Alessandro Cucchiarelli and Paola Velardi. Unsupervised named entity recognition using syntactic and semantic contextual evidence. Computational Linguistics, 2001. http://acl.ldc.upenn.edu/J/J01/J01-1005.pdf
    - Learn typical syntax/semantic context from a corpus to expand gazetteers
    - Syntactic info: elementary syntactic link (esl): Subject-Object, Noun-Preposition-Noun, etc.
    - Unknown proper noun classification: to the maximum evidence, defined by the relative plausibility of each detected esl., augmented by WordNet similarity
    - Test on Italian (Sole 24Ore) corpus and WSJ corpus: Prec and Recall both up by ~10%, 5 point increase on F-measure by WordNet context generalization

* D Nadeau et al. Unsupervised Named-Entity Recognition: Generating Gazetteers and Resolving Ambiguity. 2006. http://brown.cl.uni-heidelberg.de/~sourjiko/NER_Literatur/NER_Turney.pdf
    - Extraction (generating gazetteers): Wrapper based set expansion from few seeds, repeat retrieving Web pages and applying Web wrapper
    - Disambiguation: entity-noun ambiguity (capitalization heuristics), entity boundary detection (longest match, merge consecutive entries), entity type ambiguity (use clues in the same document, alias clues)
    - MUC 7 evaluation: Generated lists provide higher recall but lower precision.
    - Car brand evaluation: generated a list of 5,701 brands and recognition F ~ 86 
    
Product Information Extraction
------------------------------

* D. Putthividhya and J. Hu. Bootstrapped Named Entity Recognition for Product Attribute Extraction. EMNLP 2011. http://aclweb.org/anthology//D/D11/D11-1144.pdf
    - Attribute extraction from listing titles (long, little grammatical structure, errors, lack of context) by NER
    - Clothing and shoes listings from eBay, brand, garment, type/style, size, color
    - Supervised (SVM, MaxEnt) and sequential labeling by HMM (1,000 annotated items, 93.35% label classification accuracy with CRF)
    - Bootstrapping (MaxEnt, supervised) using context starting from initial seeds, with 90% precision, brand name normalization (using n-gram similarity and Jaro-Winkler distance)

* K. Mauge et al. Structuring E-Commerce Inventory. ACL 2012. http://aclweb.org/anthology//P/P12/P12-1085.pdf
    - Pattern-based property extraction (e.g., color : light blue)
    - Synonym discovery: supervised (maximum entropy) classifier over defined features with popularity (defined by # of sellers which use the attribute) and graph partitioning
    - Experiment: one-year worth (several billion) desc. of eBay listings. Prec = almost 100% up to rank 18, then drops. Synonym discovery: Prec. = 91.8% and Recall = 51%.

* K. Shinzato, S. Sekine. Unsupervised Extraction of Attributes and Their Values from Product Description. IJCNLP 2013. https://www.aclweb.org/anthology/I/I13/I13-1190.pdf
    - Build knowledge base (attribute and values) from unstructured product description, using table headers (for attribute labels) and manually crafted patterns (for values)
    - Attribute synonym discovery: pairs sharing popular values and never appear in the same structured data
    - Annotate product pages using KB (from the same genre) values, calculate the ratio MF (in desc.) and MF (in structured data) and removed high score sents.
    - Correct attribute labels = 77.6%, synonym detection purity/inv. purity = 0.920 and 0.813, extraction model (CRF) micro-averaged F = 58.15%
