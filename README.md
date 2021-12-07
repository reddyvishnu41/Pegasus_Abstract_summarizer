# Pegasus_Abstract_summarizer
It was not until the development of techniques like seq2seq learning and unsupervised language models (e.g., ELMo and BERT) that abstractive summarization becomes more feasible.
Building upon earlier breakthroughs in natural language processing (NLP) field, Google’s PEGASUS further improved the state-of-the-art (SOTA) results for abstractive summarization, in particular with low resources. To be more specific, unlike previous models, PEGASUS enables us to achieve close to SOTA results with 1,000 examples, rather than tens of thousands of training data.
And in this article, we shall look at the high level workings of PEGASUS and how it can help us in our summarization tasks.

Leaderboard on Papers With Code for abstractive summarization (as of 4 Feb 2021)
How PEGASUS works
1. Architecture
Pegasus uses encoder-decoder model
PEGASUS uses encoder-decoder model | Image by author
On a high level, PEGASUS uses an encoder-decoder model for sequence-to-sequence learning. In such a model, the encoder will first take into consideration the context of the whole input text and encode the input text into something called context vector, which is basically a numerical representation of the input text. This numerical representation will then be fed to the decoder whose job is decode the context vector to produce the summary.
In line with recent SOTA NLP models, PEGASUS also adopts the transformer architecture, and if you would like to find out more about what is a transformer, I strongly encourage you to read this article titled “The Illustrated Transformer” by Jay Alammar.
2. Pre-training
What differentiates PEGASUS from previous SOTA models is the pre-training.
The authors (Jingqing Zhang et. al.) hypothesizes that pre-training the model to output important sentences is suitable as it closely resembles what abstractive summarization needs to do. Using a metric called ROUGE1-F1, the authors were able to automate the selection of “important” sentences and perform pre-training of the model on a large corpus, i.e., 350 million web pages and 1.5 billion news articles.
With the pre-trained model, we can then perform fine-tuning of the model on the actual data which is of a much smaller quantity. In fact, evaluation results on various datasets showed that with just 1,000 training data, the model achieved comparable results to previous SOTA models. This has important practical implications as most of us will not have the resources to collect tens of thousands of document-summary pairs.

Evaluation results extracted from PEGASUS Paper
How to use Pegasus
Upon seeing the evaluation results for PEGASUS, you are probably wondering how you can write the code to use the model. Fortunately for us, Hugging Face 🤗 has PEGASUS model in-store, making it easy for us to leverage on PEGASUS.
1. Inference
To perform inference, we can follow the example script provided on Hugging Face’s website.

Screenshot of example code on Hugging Face
You can swap the model_name with various other fine-tuned models (except for google/pegasus-large) listed here, based on how similar your use case is to the dataset used for fine-tuning.

Screenshot of Pegasus models on Hugging Face
2. Fine-Tuning
If you would like to have a customized model for your use case, you can fine-tune the google/pegasus-large model on your dataset.
To do so, please refer to our Github code which we have adapted from Hugging Face’s example code on fine-tuning.

Screenshot of our PyTorch script for fine-tuning
Do however note that fine-tuning both the encoder and decoder can be very memory-intensive. If your local computer is unfortunately not up to the task (like mine 😅), you can consider using Google Cloud. And since Google Cloud has a free trial for new signups, you can experiment at no cost. 😎
