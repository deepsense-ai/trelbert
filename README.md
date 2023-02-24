# TrelBERT

TrelBERT is a BERT-based Language Model trained on data from Polish Twitter using Masked Language Modeling objective. It is based on [HerBERT](https://aclanthology.org/2021.bsnlp-1.1) model and therefore released under the same license - CC BY 4.0.
The model is available in [Hugging Face](https://huggingface.co/deepsense-ai/trelbert).

## Training

We trained our model starting from [`herbert-base-cased`](https://huggingface.co/allegro/herbert-base-cased) checkpoint and continued MLM training using data collected from Twitter.

The data we used for MLM fine-tuning was approximately 45 million Polish tweets. We trained the model for 1 epoch with a learning rate `5e-5` and batch size `2184` using AdamW optimizer.

### Preprocessing

For each Tweet, the user handles that occur in the beginning of the text were removed, as they are not part of the message content but only represent who the user is replying to. The remaining user handles were replaced by "@anonymized_account". Links were replaced with a special @URL token.

## Tokenizer

We use HerBERT tokenizer with two special tokens added for preprocessing purposes as described above (@anonymized_account, @URL). Maximum sequence length is set to 128, based on the analysis of Twitter data distribution.

## License

CC BY 4.0

## KLEJ Benchmark results

We fine-tuned TrelBERT to [KLEJ benchmark](https://klejbenchmark.com) tasks and achieved the following results:


|Task name|Score| 
|--|--|
|NKJP-NER|94.4|
|CDSC-E|93.9|
|CDSC-R|93.6|
|CBD|76.1|
|PolEmo2.0-IN|89.3|
|PolEmo2.0-OUT|78.1|
|DYK|67.4|
|PSC|95.7|
|AR|86.1|
|__Average__|__86.1__|

For fine-tuning to KLEJ tasks we used [Polish RoBERTa](https://github.com/sdadas/polish-roberta) scripts, which we modified to use `transformers` library. For the CBD task, we set the maximum sequence length to 128 and implemented the same preprocessing procedure as in the MLM phase.

Our model achieved 1st place in cyberbullying detection (CBD) task in the [KLEJ leaderboard](https://klejbenchmark.com/leaderboard). Overall, it reached 7th place, just below HerBERT model.

## Authors
deepsense.ai
Wojciech Szmyd, Alicja Kotyla, Michał Zobniów, Piotr Falkiewicz, Jakub Bartczuk, Artur Zygadło

For more information, reach out to us via e-mail: artur.zygadlo@deepsense.ai
