---
title: "Paper Summary of Using Reccurent Neural Networks for Slot Filling in Spoken Language Understanding"
date: 2017-11-18
---

================
Grégoire Mesnil, Yann Dauphin, Kaisheng Yao, Yoshua Bengio, Li Deng, Dilek Hakkani-Tur, Xiaodong He, Larry Heck, Gokhan Tur, Dong Yu, Geoffrey Zweig.  
IEEE/ACM TRANSACTIONS ON AUDIO, SPEECH, AND LANGUAGE PROCESSING, VOL. 23, NO. 3, MARCH 2015  
A link to this paper is [**here**](http://ieeexplore.ieee.org/document/6998838/?reload=true).  

### Background
Slot filling is one the key problems in "spoken language understanding" (SLU). Typically, SLU consists of three sub-tasks: domain detection, intent determination and slot filling. It can convert the speech recognition results of users' utterances into users' intent along with specific meta-information included such as departure city and arrival city (example below) so that the dialogue manager can decide the most approiate action based on that. If you are developing an Alexa skill or Google Home application, you will see they similarly require you to specify all the possible user intents. And under each intent, you also need to give sample user utterances and highlight the words which corresponding to the slot types you need.  

Below is an example sentence with domain, intent, typical domain-independent named entities and slot/concept annotations illustrated in the popular in/out/begin (IOB) representation.  

![bias](/assets/IOB_example.png)  

Standard approaches to solving the slot filling problem include generative models such as HMM/CFG composite models, hidden vector state (HVS) model and discriminative models such as CRFs and SVMs. While domain detection, intent determination have been well solved with deep learning methods, this paper basicly implemented and compared several recurrent neural network architectures and their variations.  

### Key idea  
**Word Embeddings**    
The embedding matrix can be initialized with pretrained values on an external dataset (GloVe, word2vec) or initialized from random values. This paper found these two mothods led to the same results on the ATIS dataset. But if we try to do transfering training which means our testing data is from a different dataset as training data, I think we do need pretrained word embedding values for initialization and only train the most K frequent words in our training dataset.

**Context Word Window**    
This paper used a context word window as the input for the RNNs.  

$$ C_d(l_{i-d}^{i+d}) = \tilde{E}\tilde{l}_{i-d}^{i+d} \in \rm I\!R $$ 

where $$\tilde{E}$$ corresponds to the embedding matrix $$E$$ replicated vertically $$2d + 1$$ times and $$\tilde{l}_{i-d}^{i+d}$$ corresponds to the concatenation of one-hot word index vectors.
This gives us the word embedding vectors of the d-context word window ($$2d+1$$ words). But I think if we introduce temporal feedback using bidirectional LSTM, it's not necessary to use word window as input.

**Elman, Jordan and Hybrid Architectures**  
Just like the basic RNNs we discussed in class, the Elman RNN dynamics can be written as:  

$$ 
\begin{align*}
	h^{(1)}(t) &= f(U^{(1)}C_d(l_{t-d}^{t+d}) + U'^{(1)}h^{(1)}(t-1))  \\
	h^{(n+1)}(t) &= f(U^{n+1}h^{(n)}(t) + U'^{(n+1)}h^{(n+1)}(t-1))
\end{align*}
$$ 

The Jordan RNN is similar to the Elman RNN except the recurrent connections take their input from the output posterior probabilities:  

$$ h(t) = f(UC_d(l_{t-d}^{t+d}) + U'P(y(t-1))) $$ 

And the hybrid version of the Elman-type and Jordan-type:

$$ h(t) = f(UC_d(l_{t-d}^{t+d}) + U'P(y(t-1)) + U^*h(t-1)) $$ 

The forward, backward and bidirectional variant:  

$$ 
\begin{align*}
	\overrightarrow{h}(t) &= f(\overrightarrow{U}C_d(l_{t-d}^{t+d}) + \overrightarrow{U}'\overrightarrow{h}(t-1))  \\
	\overleftarrow{h}(t) &= f(\overleftarrow{U}C_d(l_{t-d}^{t+d}) + \overleftarrow{U}'\overleftarrow{h}(t+1))  \\
	\overleftrightarrow{h}(t) &= f(BC_d(l_{t-d}^{t+d}) + B'\overrightarrow{h}(t-1) + B^*\overleftarrow{h}(t+1))
\end{align*}
$$  

Similar to Maximum Entropy Markov Model, because of the possibility local normalization, the RNNs suffer from the same label bias problem. To alleviate this, this paper proposed two methods: slot language models and recurrent CRFs.  
  
**Slot Language Models**  
To approximate CRF, this paper applied the Viterbi algorithm using the tag level posterior probabilities obtained from the RNN. And the state observation likelihoods are as follow: 

$$ 
\begin{align*}
	\tilde{S} &= arg max_SP(S|L)  \\
			  &= arg max_SP_{LM}(S)^\alpha \times P(L|S)  \\
			  &\sim arg max_SP_{LM}(S)^\alpha  \\
			  &\times \prod_tP_{RecNN}(s_t|l_t) / P(s_t)  
\end{align*}
$$ 

I am not sure about how to get $$P(s_t)$$, maybe the proportion of that tag in the training data?

**Recurrent CRF**  
This method takes advantage of the sequence-level discrimination ability of the CRF and the feature learning ability of the RNN. The conditional probability of a slot sequence is as folow:  

$$ 
\begin{align*}
	P(S_1^N|L_1^N) &= \frac{1}{Z} \prod_{t=1}^N e^{H(s_{t-1}, s_t, l_{t-d}^{t+d})}  \\
	H(s_{t-1}, s_t, l_{t-d}^{t+d}) &= \sum_{m=1}^M \lambda_m h_m (s_{t-1} ,s_t, l_0^{t+d})  \\
								   &= \sum_{p=1}^P \lambda_p h_p (s_{t-1} ,s_t) + \sum_{q=1}^Q \lambda_q h_q (s_{t} ,l_0^{t+d})
\end{align*}
$$ 

### Discussion
In all, the RNNs used in this paper are still the state-of-the-art method of the slot-filling problem. It did have an improvement compared to the CRF baseline. But this paper didn't mention the vanishing gradients problem of RNNs. To avoid this, we may use LSTM or GRU instead of Elman or Jordan RNNs in our final project. Also, RNNs require a large training dataset while it is hard to get enough training data in a specific domain to train such a model in practice.