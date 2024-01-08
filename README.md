# Advanced Machine Translation university assignments

This project consists of training several neural MT and language models using fine-tuning techniques in order to assess and compare their performance in EN-DE translation and ultimately to produce a benchmark of performance results. All approaches and performance assessment techniques are briefly described below.

## Baseline vs. fine-tuned mBART

This approach compares Facebook's **multilingual BART model** available on HuggingFace (facebook/mbart-large-50-many-to-many-mmt) with a fine-tuned version of it. The fine-tunining is done using a shortened version of the EMEA medical corpus (https://opus.nlpl.eu/EMEA.php).

## Freezing mBART's encoder & embeddings

This approach leverages the Domain Adaptation technique of freezing parameters by freezing mBART's encoder and embeddings.

Freeze certain parameters during domain adaptation helps preserves a model'S knowledge learned from the source domain. This can be beneficial if some features or patterns learned in the source domain are still relevant or transferable to the target domain. It also helps prevent catastrophic forgetting, where the model forgets what it learned from the source domain when adapting to the target domain. By keeping certain parameters fixed, the model retains its ability to perform well on the source domain while adapting to the new data.

## Baseline vs. fine-tuned Distilled NLLB

This approach compares the performance of Facebook's **distilled No Language Left Behind (NLLB)** model available on HuggingFace (facebook/nllb-200-distilled-600M) with a fine-tuned version of it. The key idea behind model distillation is to create a more efficient and compact model that retains the essential knowledge of the larger model, making it suitable for deployment on resource-constrained devices or scenarios where computational efficiency is crucial. This is done using teacher-student learning, where a large, complex model (teacher model) is used to train a smaller, more lightweight model (student model) to replicate the behavior of the larger model.

## Translating using language models: FLAN-T5

In this approach translation using Google's **FLAN-T5 language model** available on HuggingFace (google/flan-t5-large) is attempted. Techniques such as *beam search*, a decoding algorithm commonly used in sequence-to-sequence tasks, and *Minimum Bayes Risk (MBR)* (https://github.com/ZurichNLP/mbr), a decoding algorithm used to make decoding decisions based on the expected risk or cost, rather than simply choosing the most likely output sequence according to the model's probabilities, are implemented.


# Evaluation Metrics

For evaluations, the BLEU-score, the CHaRacter-level F-score (chrF) and the COMET score are used. All models were evaluated on a very shortened version (about 100 sentences) of the Medline medical corpus (https://www.nlm.nih.gov/databases/download/pubmed_medline.html). 

**BLEU**: a metric used for evaluating the quality of machine-generated translations by comparing them to one or more reference translations

**chrF**: a metric used for evaluating the quality of machine-generated translations in NLP, particularly in the context of MT. The chrF score is designed to address some of the limitations of traditional n-gram-based metrics like BLEU by focusing on character-level rather than word-level evaluation.
While BLEU primarily operates at the word level, chrF focuses on character-level evaluation. It considers the overlap of character n-grams between the candidate and reference translations.

**COMET**: a new neural framework for training multilingual machine translation (MT) evaluation models, designed to predict human judgments of MT quality (such as MQM scores). Compared to traditional metrics like the one above, the COMET score is more similar to human judgement.

# The Benchmark

| Model                    | BLEU | chrF | COMET  |
|--------------------------|-----------|-----------|--------|
| mBART                    | 23.8      | 46.8      | 0.705  |
| Finetune mBART           | 24.8      | 47.9      | 0.721  |
| Emb mBART                | 24.6      | 47.2      | 0.718  |
| enc mBART                | 24.8      | 47.3      | 0.716  |
| emb/enc mBART            | 23.9      | 47.2      | 0.716  |
| Distil NLLB              | 23.8      | 47.1      | 0.725  |
| Finetune distil NLLB     | 23.7      | 47.4      | 0.719  |
| LLM zero-shot (T5), Beam n=5 | 14.5   | 39.3      | 0.648  |
| LLM mbr                  | 17.7      | 44.4      | 0.669  |
