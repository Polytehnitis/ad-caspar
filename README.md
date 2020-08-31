# AD-CASPAR

This is the repository of the Python (3.7+) implementation of AD-CASPAR (Abductive-Deductive Cognitive Architecture System Planned and Reactive)
referred to the paper _AD-CASPAR: Abductive-Deductive Cognitive Architecture based on Natural Language and First Order Logic Reasoning_. 
This architecture inherits all the features of his predecessor [CASPAR](https://github.com/fabiuslongo/pycaspar), extending them with a 
 two-level Clauses Knowledge Base, an abductive inference as pre-phase of deduction, and a Telegram
chatbot prototype implementing Question Answering tecniques for Polar and Wh-Questions.

![Image 1](https://github.com/fabiuslongo/ad-caspar/blob/master/images/AD-Caspar.jpg)

# Installation


This repository has been tested on Pycharm 2019.1.2 x64 with the following packages versions:

* [Phidias](https://github.com/corradosantoro/phidias) (release 1.3.4.alpha) 
* SpaCy (ver. 2.2.4)
* Natural Language Toolkit (ver. 3.5)
* python-telegram-bot
* [Mongodb](www.mongodb.com)

### Phidias

---------------
##### on all platforms
```sh
> git clone https://github.com/corradosantoro/phidias
> python setup.py install
```
##### additional package needed (Linux)
```sh
> python -pip install readline
> python -pip install parse
```
##### additional package needed (Windows)
```sh
> python -m pip install pyreadline
> python -m pip install parse
```

### SpaCy

---------------

```sh
> python -m pip install spacy
> python -m spacy download en_core_web_md
```


### Natural Language Toolkit

---------------

from prompt:
```sh
> python -m pip install nltk
```
from python console:
```sh
> import nltk
> nltk.download('wordnet')
```

### python-telegram-bot
```sh
> python -m pip python-telegram-bot
```

# Testing
Before going any further it is first necessary to create a new telegram bot by following the instruction
 in this [page](https://core.telegram.org/bots#6-botfather). The returned token must be inserted instead of 
 XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX at line 82 of sensors.py. 


### Starting Phidias Shell

---------------

```sh
> python ad-caspar.py

          PHIDIAS Release 1.3.4.alpha (deepcopy-->clone,micropython,py3)
          Autonomous and Robotic Systems Laboratory
          Department of Mathematics and Informatics
          University of Catania, Italy (santoro@dmi.unict.it)
          
eShell: main >
```
### Starting agent

---------------

```sh
eShell: main > go()
eShell: main > AD-Caspar started! Bot is running...
```

### Inspecting Knowledge Bases

---------------

After the agent is started, the Belief KB can be inspected with the following command:

```sh
eShell: main > kb
WAIT(1000)
eShell: main >
```
The value inside the belief WAIN represent the maximum duration of each session. It can be changed by modifing the value
of the variable WAIT_TIME (section AGENT) in config.ini. The two layers of the Clauses KB (respectively High KB and Low KB) can be inspected with the following commands:

```sh
eShell: main > hkb()
0 clauses in Higher Knowledge Base
eShell: main > lkb()
0  clauses in Lower Knowledge Base
eShell: main >
```

both High KB e Low KB can be emptied with the following commands:

```sh
eShell: main > chkb()
Higher Clauses kb initialized.
0  clauses deleted.
eShell: main > clkb()
Lower Clauses kb initialized.
0  clauses deleted.
eShell: main >
```

to start a session you have to go to the telegram bot window and type the word "hello". Assertions must end with 
"." and questions must end with "?". Otherwise the utterances will be processed as direct commands or routines (check out the page of [CASPAR](https://github.com/fabiuslongo/pycaspar) for details).

![Image 2](https://github.com/fabiuslongo/ad-caspar/blob/master/images/start-assertion.JPG)

After such interaction withe the telegram bot, the two layers of the Clauses KB will be as it follows:

```sh
eShell: main > hkb()
eShell: main > In_IN(Become_VBD(Barack_NNP_Obama_NNP(x1), Of_IN(President_NN(x2), United_NNP_States_NNP(x3))), N2009_CD(x4))

1 clauses in Higher Knowledge Base

eShell: main > lkb()

In_IN(Become_VBD(Barack_NNP_Obama_NNP(x1), Of_IN(President_NN(x2), United_NNP_States_NNP(x3))), N2009_CD(x4))
['In_IN', 'Become_VBD', 'Barack_NNP_Obama_NNP', 'Of_IN', 'President_NN', 'United_NNP_States_NNP', 'N2009_CD']
Barack Obama became the president of United States in 2009.

1  clauses in Lower Knowledge Base
```
