## Topic Depth Dataset
[日本語 README](https://github.com/IshiguroLab/TopicDepthDataset/blob/c45b3cf545c54788ff495f5efb1898b1d10f6f4f/README_JP.md)

The Topic Depth Dataset is a collection of 1,600 topics (questions) with labeled depth information, presented in Japanese.

Reference：Papre (English), [Paper (Japanese)](https://www.anlp.jp/proceedings/annual_meeting/2024/pdf_dir/B11-5.pdf)，[Data](https://github.com/IshiguroLab/TopicDepthDataset/tree/main/data)

## Fine-tuning
Download `train.jsonl` and `test.jsonl` and execute the following code:

```
from openai import OpenAI
client = OpenAI(api_key='your_api_key')

train_file = client.files.create(
    file=open('train.jsonl', 'rb'),
    purpose='fine-tune'
)

test_file = client.files.create(
    file=open('test.jsonl', 'rb'),
    purpose='fine-tune'
)

train_file_id = train_file.id
valid_file_id = test_file.id
model = 'gpt-3.5-turbo'

client.fine_tuning.jobs.create(
    training_file = train_file_id,
    validation_file = valid_file_id,
    suffix = 'suffix_name',
    model = model
)
```
Note: During my trial, it cost approximately 500 yen per epoch, resulting in about 1,500 yen for 3 epochs of training.

## Citation
Seiya Mitsuno, Midori Ban, Hiroshi Ishiguro, and Yuichiro Yoshikawa. 2024. “Deepening Conversations over Time: A Chatbot with a Topic Depth Estimation Model for Gradually Engaging in Deeper Chats.” In 2024 33rd IEEE International Conference on Robot and Human Interactive Communication (ROMAN), 1354–61. IEEE.

```
@INPROCEEDINGS{Mitsuno2024-ev,
  title     = "Deepening conversations over time: A chatbot with a topic depth
               estimation model for gradually engaging in deeper chats",
  author    = "Mitsuno, Seiya and Ban, Midori and Ishiguro, Hiroshi and
               Yoshikawa, Yuichiro",
  booktitle = "2024 33rd IEEE International Conference on Robot and Human
               Interactive Communication (ROMAN)",
  publisher = "IEEE",
  pages     = "1354--1361",
  month     =  aug,
  year      =  2024
}
```

## Acknowldegment
This work was supported by JSPS KAKENHI under Grant JP20H00101, JP19H05691, JP23KJ1462, and Innovation Platform for Society 5.0 (Ministry of Education, Culture, Sports, Science and Technology) under Grant JPMXP0518071489.
