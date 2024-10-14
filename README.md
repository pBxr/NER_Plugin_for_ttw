# Test Environment for a TagTool_WiZArD Named Entity Recognition Plugin

## Introductory remarks

In the long run `TagTool_WiZArD application (ttw)` (see https://github.com/pBxr/TagTool_WiZArd) shall be enabled to integrate Natural Language Processing features. In this first step an environment is beeing created in which Named Entity Recognition processes can be tested using the `Hugging Face` `Transformers` pipeline (see https://huggingface.co) and a variant of the `BERT` language model family (see below). 

The final aim is to create a plugin for the productive version of `ttw` application.

## Approach

In this version the focus lies on the extraction of location names. To be able to vary and to handle the test environments in a simple way the `Anaconda` plattform (see https://www.anaconda.com/) is used in combination with `Jupyter Notebooks` where the `Python` code is run.    
- It is simulated that the plugin receives path, name of the text file and further settings from `ttw`.
- The plugin gets the plain text from the selected text file and saves it in a folder ("NER_results"). 
- It extracts a tokenized list of result entries that are beeing re-merged to a list of place names.
- The place names are run through the `iDAI.gazetteer` webservice to identify the locations and extract the gazetteer-IDs, that `ttw` needs as `.csv` list to enrich the article file with geographic authority data (see also https://github.com/pBxr/ID_Extractor for `ttw`).
- A log file with the tokenized results, a draft for the final `.csv` list and the complete gazetteer query result as `.json` file will be saved in the NER_results folder.

## Technical details

- `dslim/bert-base-NER` is very suitable for this testing purposes concerning its performance and accuracy. 
Here are the main environments parameters this version is tested with:
- `Anaconda Navigator 2.6.0` (`Windows`)
- `Python 3.7.0`
- `PyTorch 1.4.0`
- `TensorFlow 2.3.0`
- `Transformers 4.11.3`
- For all other questions see especially https://huggingface.co/docs/transformers/installation.
- In case of problems check whether to use pip or conda-forge channel to install components. 

## Other Aspects

- The NER results show quality differences that seem to depend on the state of the plain text (with or without title, keywords and abstracts, extracted with `bs4` from structured text files or from plain text etc.). So the pre-processing of the texts needs more focus.
- The insufficient quality of the `iDAI.gazetteer` query results was ignored for this first test version (as well as the webservice´s default query limit). To work on filter mechanisms to improve the quality of the result will be a task for forthcoming commits.
