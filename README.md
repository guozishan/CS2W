# CS2W

<p align="center">
    <a href="#introduction">Introduction</a> •
    <a href="#dataset-analysis">Dataset Analysis</a> •
    <a href="#docs">Docs</a> •  
    <a href="#how-to-use-cs2w">How to use CS2W</a> •
    <a href="#data-field-description">Data Field Description</a> •
    <a href="#citation">Citation</a>
</p>


## introduction

Spoken texts (either manual or automatic transcriptions from automatic speech recognition (ASR)) often contain disfluencies and grammatical errors, which pose tremendous challenges to downstream tasks. Converting spoken into written language is hence desirable. Unfortunately, the availability of datasets for this is limited. To address this issue, we present **[CS2W](https://aclanthology.org/2023.emnlp-main.241.pdf), a Chinese Spoken-to-Writtenstyle conversion dataset** comprising 7,237 spoken sentences extracted from transcribed conversational texts. Four types of conversion problems are covered in CS2W: disfluencies, grammatical errors, ASR transcription errors, and colloquial words. 

## Dataset Analysis

### Overall Statistics

|                  | Train   | Dev    | Test   | All     |
| ---------------- | ------- | ------ | ------ | ------- |
| \#sentences      | 5,789   | 724    | 724    | 7,237   |
| w/ 1 error       | 4,211   | 596    | 597    | 5,404   |
| w/ 2 error       | 1,069   | 107    | 112    | 1,288   |
| w/ 3 error       | 317     | 15     | 11     | 343     |
| w/ 4 error       | 192     | 6      | 4      | 202     |
| \#Spans          | 8,022   | 889    | 881    | 9,792   |
| Avg. #spans      | 1.386   | 1.228  | 1.217  | 1.353   |
| Avg. Spans_len   | 2.003   | 1.883  | 2.069  | 2.020   |
| \#Characters     | 121,907 | 10,844 | 10,987 | 143,738 |
| Avg. #characters | 21.058  | 15.033 | 15.175 | 19.862  |
| \#Tokens         | 78,549  | 7,120  | 7,116  | 92,785  |
| Avg. #tokens     | 13.569  | 9.834  | 9.829  | 12.821  |

### Conversion Type Distribution

| First Level              | Second Level         | Proportion |
| ------------------------ | -------------------- | ---------- |
| Disfluency               | R-type               | 64.62%     |
|                          | Filler words         | 19.09%     |
| ASR Transcription Errors | -                    | 0.70%      |
| Grammatical Errors       | Missing Words        | 2.92%      |
|                          | Redundant Words      | 5.22%      |
|                          | Incorrect Word Order | 0.23%      |
| Colloquial Words         | -                    | 7.22%      |

## Docs

Below is the documentation tree, giving you an overview of the directory structure and the purpose of each file:

```
+-- data 
|   +-- train.jsonl
|   +-- val.jsonl
|   +-- test.jsonl
+-- README.md
```

## How to use CS2W

First, clone this repository using the following command:

```
git clone https://github.com/guozishan/CS2W.git
```

Then, load the data using Python's built-in `json` package as shown below:

```python
import json

fin = open("path/to/CS2W/data/train.jsonl", mode="r", encoding="utf-8")

for json_line in fin:
    json_data = json.loads(json_line)
    print(json_data)
```

## Data Field Description

| Field Name                | Data Type | Description                                                  |
| ------------------------- | --------- | ------------------------------------------------------------ |
| `id`                      | Integer   | Unique identifier for the data                               |
| `content`                 | String    | The source content of the text (spoken language)             |
| `disfluency_label`        | String    | Label indicating the type of Disfluency conversion (1: Filler words, 2: R-type, 0: Normal) |
| `grammatical_error_label` | String    | Label indicating the type of Grammatical Errors conversion (1: Redundant Words, 2: Missing Words, 0: Normal) |
| `colloquial_word_label`   | String    | Label indicating the type of Colloquial Words conversion (1: Colloquial Words, 0: Normal) |
| `asr_error_label`         | String    | Label indicating the type of ASR Transcription Errors conversion (1: ASR Transcription Errors, 0: Normal) |
| `disfluency_num`          | Integer   | The count of Disfluency type conversions in the text         |
| `grammatical_error_num`   | Integer   | The count of Grammatical Errors type conversions in the text |
| `colloquial_word_num`     | Integer   | The count of Colloquial Words type conversions in the text   |
| `asr_error_num`           | Integer   | The count of ASR Transcription Errors type conversions in the text |
| `ref`                     | String    | The target content of the text (written language)            |

```json
{
    "id": 3,
    "content": "这个事情也是值得大家应，值得大家注意的",
    "disfluency_label": "0000002222200000000",
    "grammatical_error_label": "0000000000000000000",
    "colloquial_word_label": "0000000000000000000",
    "asr_error_label": "0000000000000000000",
    "disfluency_num": 1,
    "grammatical_error_num": 0,
    "colloquial_word_num": 0,
    "asr_error_num": 0,
    "ref": "这个事情也是值得大家注意的"
}
```

## Data License

Attribution-ShareAlike 4.0 International (CC BY-SA 4.0) license. (License URL: https://creativecommons.org/licenses/by-sa/4.0/)

## Citation

```
inproceedings{guo2023cs2w,
  title={CS2W: A Chinese Spoken-to-Written Style Conversion Dataset with Multiple Conversion Types},
  author={Guo, Zishan and Yu, Linhao and Xu, Minghui and Jin, Renren and Xiong, Deyi},
  booktitle={Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing},
  pages={3962--3979},
  year={2023}
}
```

