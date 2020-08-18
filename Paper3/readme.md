 # Detecting Code Comment Inconsistency using Siamese Recurrent Network


 ## Authors

 Fazle Rabbi

 ![Authors Avatar](./image1.jpg)

  Md Saeed Siddik

![Authors Avatar](./image2.jpg)


 ## Track:  ICPC 2020 ERA


## On
Wed 15 Jul 2020 02:15 - 02:30 at ICPC - Session 10: Documentation Chair(s): Gias Uddin


## Abstract:

Comments are the internal documentation of corresponding code blocks, which are essential to understand and maintain a software. In large scale software development, developers need to analyze existing codes, where comments assist better readability. In practice, developers commonly ignore comments’ updating with respect to changing codes, which leads the code comment inconsistency. Traditionally researchers detect these inconsistencies based on codecomment tokens. However, sequence ordering in codecomments is ignored in existing solution, as a result inconsistencies for invalid sequences of codes and comments are neglected. This paper solves these inconsistencies using siamese recurrent network which uses word tokens in codes and comments as well as their sequences in corresponding codes or comments. Proposed approach has been evaluated with a benchmark dataset, along with the ability of detecting invalid code comment sequence is examined.
As a result, it misleads the new developers and later may introduce
bugs. So, if a system can automatically detect the inconsistency
between comment and source code and warn a developer about the
inconsistency, the developer can decide which comment should be
followed and which one should be avoided.
Previously a work is proposed [2] to predict code comment
coherent using Support Vector Machine over Vector Space Model of
tf-idf. However, to measure how a code and a comment are coherent
to each other, the ordering of used words should also be considered.
Because, changing ordering of words in a code/comment can change
the meaning of the corresponding code/comment. This important
issue is missing in the mentioned paper.
In this work, an automatic system is proposed where a siamese
recurrent network is used to understand codes and comments and
find inconsistency between them. The proposed system converts a
code and comment into vectors to compare their similarity. As the
sequence of words in a code or comment are tracked, the system
can detect inconsistency when those are not in a valid sequence.
To understand the overall system better, some background knowl-
edge is necessary related to Abstract Syntax Tree (AST), Recurrent

Neural Network (RNN), Long Short Term Memory (LSTM) etc. In
this work, AST is used to turned structured code sequences into

sentences and RNN-LSTM is used to developing the siamese net-
work.
The newly proposed code comment inconsistency approach has
been experimented with publicly available Java code-comment
pairs dataset and siamese network. This section elaborates those
experimental details and statistical findings accordingly.