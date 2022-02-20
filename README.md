# NER_SW_Fanfic
NER on Star Wars fan fiction using spaCy and gensim word vectors


In my pursuit of learning NLP, I decided to try some NER modeling on my own Star Wars fan fiction. I like using my own writing (fiction and non-fiction) for personal NLP projects because there's a fair amount of it, it's readily available, and it's fun. I decided my Star Wars fan fiction was a good choice for NER since there are a lot of entities and many of them are things that a standard off-the-shelf model wouldn't pick up and/or label correctly, like original or obacure character names and places, or specific types of entities like droids and species. 

This project is broken into four notebooks. The first notebook shows file importation, data cleaning, and splitting the corpus into training and testing data.

The second notebook uses the training data to build word vectors with gensim. The code is there to do unigrams, bigrams, and trigrams. 

The third notebook takes the training data and uses spaCy's entity ruler to create some specific labels to annote the data. It is not a full dramatis personae of every character and entity. But it does include ones that are particularly odd, and that earlier versions of the models were getting consistently wrong. For example, 'Han' is a specific entity labeled as PERSON. Early models kept labeling Han as a NORP, which makes sense if it thought it meant Han Chinese. Other specific labels include SPECIES, DROID, FORCE as it's own label, and FORM for different lightsaber comabt forms. The training data are annotated, converted to spaCy 3 format, and split into training and validation data.

The fourth notebook reloads the word vectors and adds the NER pipe to the model, showing the command line instruction in the notebook. The model is then trained, again showing the comand line instruction in the notebook with the output. The best model is reloaded and tested on the hold out data from Notebook 1. 

The tested output uses displacy's entity rendering to show which entities got labeled from those 50 lines. Many were PERSON enities that were called out in the annotated data, while some were not, notably 'Kalick,' 'Adan,' 'Sheev Palpatine,' and, most interestingly, 'Dathomiri Nightsisters.' I am pretty sure this is the only time the bigram appears in the entire corpus of over 18 thousand sentences, so I thought it was interesting that got picked up. 

This model used word vectors and bigrams. Trigrams didn't seem to improve the model very much. The original model that had less good text cleaning, no word vectors, and fewer entities explicitly annotated had an f1 score around .83. The current model has an f1 score of .946 and a PERSON f1 score of .978. 
