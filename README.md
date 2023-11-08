# Experiment-6---Implementation-of-Semantic-Analysis

## Aim : 
Construct a python program to read a text from a file.Identify the verbs from the text file and provide synonyms for all verbs using Natutal Language Processing 

## Algorithm:
1.Install the required libraries: Install nltk (Natural Language Toolkit) by running pip install nltk in your terminal. Install WordNet by running nltk.download('wordnet') in your Python script or notebook.

2.Import the necessary libraries and modules.

3.Read the text file.

4.Tokenize the text into sentences and words.

5.Identify verbs using part-of-speech tagging.

6.Get synonyms for each verb.

7.Process the text file and display the verbs and their synonyms.

## Program:
```
import nltk
import csv
from nltk.corpus import wordnet

nltk.download('averaged_perceptron_tagger')
nltk.download('wordnet')
nltk.download('punkt')

# Function to identify verbs in a sentence
def get_verbs(sentence):
    verbs = []
    pos_tags = nltk.pos_tag(nltk.word_tokenize(sentence))
    for word, tag in pos_tags:
        if tag.startswith('V'):  # Verbs start with 'V' in the POS tag
            verbs.append(word)
    return verbs


def get_synonyms(word):
    synonyms = []
    for syn in wordnet.synsets(word):
        for lemma in syn.lemmas():
            synonyms.append(lemma.name())
    return synonyms


def read_text_file(file_path):
    with open(file_path, 'r') as file:
        text = file.read()
    return text


def main():
    file_path = 'sample.txt'

    text = read_text_file(file_path)
    sentences = nltk.sent_tokenize(text)

    all_verbs = []
    synonyms_dict = {}

    for sentence in sentences:
        verbs = get_verbs(sentence)
        all_verbs.extend(verbs)
        for verb in verbs:
            synonyms = get_synonyms(verb)
            synonyms_dict[verb] = synonyms

    with open('output.csv', 'w', newline='') as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(['Verb', 'Synonyms'])
        for verb, synonyms in synonyms_dict.items():
            writer.writerow([verb, ', '.join(synonyms)])

if __name__ == '__main__':
    main()

```
## Output:
![image](https://github.com/s-adhithya/Experiment-6---Implementation-of-Semantic-Analysis/assets/113497423/ed6d7e28-1771-49a5-979d-8fd2d28f12dc)

## Result
Thus, we have successfully implemented a program for Natural Language Processing.
