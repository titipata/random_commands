[back to home](../README.md)

# Stanford NLP

I would like to use Stanford Core NLP (on EC2 Ubuntu instance) for multiple of
my text preprocessing which includes [Core NLP](http://stanfordnlp.github.io/CoreNLP/),
[Named Entiry Recognizer (NER)](http://nlp.stanford.edu/software/CRF-NER.html) and
[Open IE](http://nlp.stanford.edu/software/openie.html). Basically I want to create
server and can be able to query it with Python easily.

I haven't done all the installation process yet. However, I want to put everything in one place
so I can come back later to update this post.

First, they require Java 1.8 or later. We can do as follows

```bash
sudo add-apt-repository ppa:webupd8team/java -y
sudo apt-get update
sudo apt-get install oracle-java8-installer
sudo apt-get install oracle-java8-set-default
```

Then I can add `export JAVA_HOME=/usr/lib/jvm/java-8-oracle` into my `.bash_profile`.
Now, when I type `java -version`, it should return version 1.8

Now, we just have to download [Core NLP](http://stanfordnlp.github.io/CoreNLP/),
[Named Entiry Recognizer (NER)](http://nlp.stanford.edu/software/CRF-NER.html) and
[Open IE](http://nlp.stanford.edu/software/openie.html) `.jar` file. I simply put
every `jar` file in one place.

Now, I have to start the server (the full documentation is at this [page](http://stanfordnlp.github.io/CoreNLP/corenlp-server.html)) as an API so I can
query from this server later on. I use `screen` to run
the server in case I want to exit from my EC2 instance.

```bash
screen # start screen
export CLASSPATH="`find . -name '*.jar'`"
java -mx4g -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLPServer [port?] # run server
```

Then in screen, I can use `ctrl+a` and `d` in order to detach from my screen
(simply use `screen -r <port_name>` to access the opening screen, `screen -ls` to list).
Then after running the server, I can simply go to `<ec2_ip>:9000` in order to test the server.

Now, we have to just find the right Python wrapper for CoreNLP. There are a bunch including
[dasmith/stanford-corenlp-python](https://github.com/dasmith/stanford-corenlp-python),
[smilli/py-corenlp](https://github.com/smilli/py-corenlp), [dat/pyner](https://github.com/dat/pyner)
and [more](http://stanfordnlp.github.io/CoreNLP/other-languages.html).


### Install on Mac OSX

I did similar to what I did on Amazon EC2. However, the process is less complicated.
I just have to download the file from [CoreNLP page](http://stanfordnlp.github.io/CoreNLP/).
Then running the same way as on Amazon EC2 Ubuntu.

```bash
screen # start screen
export CLASSPATH="`find . -name '*.jar'`"
java -mx4g -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLPServer [port?] # run server
```


## Usage

In my opinion, [smilli/py-corenlp](https://github.com/smilli/py-corenlp)
is one of the easiest Python library to use. You can install using `pip` i.e.
`pip install pycorenlp`. An example usage is as below:


```python
from pycorenlp import StanfordCoreNLP
nlp = StanfordCoreNLP('http://localhost:9000')
output = nlp.annotate('Department of Radiation Oncology, Stanford University, Aviano, PN, Italy',
    properties={
      'annotators': 'ner',
      'outputFormat': 'json'}
    )
```

where we can find all support annotators from this [page](http://stanfordnlp.github.io/CoreNLP/simple.html) or from this [page](http://stanfordnlp.github.io/CoreNLP/annotators.html). We can state multiple annotators by just using commas e.g. `ner,openie`. For output format, it can be `json`, `xml`, `text` or `serialized` (see more from [CoreNLP server page](http://stanfordnlp.github.io/CoreNLP/corenlp-server.html)).

So yeah, at the end, it's not that hard to run Stanford CoreNLP server and annotate some text that we have!


### Example for sentence split

Here is one example on how to use `StanfordCoreNLP` to do sentence split.

```python
from pycorenlp import StanfordCoreNLP
nlp = StanfordCoreNLP('http://localhost:9000')

properties={
  'annotators': 'ssplit',
  'outputFormat': 'json'
  }

def sentence_split(text, properties={'annotators': 'ssplit', 'outputFormat': 'json'}):
    """Split sentence using Stanford NLP"""
    annotated = nlp.annotate(text, properties)
    sentence_split = list()
    for sentence in annotated['sentences']:
        s = [t['word'] for t in sentence['tokens']]
        sentence_split.append(s)
    return sentence_split

# example
text = 'Hello all. My name is Titipat, the best LoL player.'
sentence_split(text)
```
