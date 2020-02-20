# initial

## Datasets

https://grouplens.org/datasets/movielens/


## Analyzers

What can analyzers do? 

- Character Filters 
	- remove HTML encoding, convert & to and
- Tokenizer
	- Split strings on whitepace / punctuations / non-letters
- Token Filter
	- Lowercasing, 
	- stemming (box - boxing, boxed) 
	- synonyms (big - large, huge) 
	- stopwords (the, and, a)

Standard Analyzers

- standard
	- split on word boundaries, good if language is unknown
- simple
	- splits on anything isn't a letter
- whitespace
	- any punctuation is preserved
- language
	- accounts for language-specific stopwords / stemming