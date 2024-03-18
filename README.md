## Topic Depth Dataset
The Topic Depth Dataset is a collection of 1,600 topics (questions) with labeled depth information, presented in Japanese.
Note that, this dataset is 

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

## Acknowldegment
This work was supported by JSPS KAKENHI under Grant JP20H00101, JP19H05691, JP23KJ1462, and Innovation Platform for Society 5.0 (Ministry of Education, Culture, Sports, Science and Technology) under Grant JPMXP0518071489.
