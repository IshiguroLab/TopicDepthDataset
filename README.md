## 話題の深さデータセット
話題の深さデータセット（Topic Depth Dataset）は，1,600話題（質問文）について，その深さをラベル付けしたデータセットです．

参考：論文，[データ](https://github.com/IshiguroLab/TopicDepthDataset/tree/main/data)

## Fine-tuning
train.jsonlとtest.jsonlをダウンロードして，以下のコードを実行．
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
※私が試したときは，1epochあたり約500円程で，3epochの学習となったため約1,500円程の費用が掛かりました．

## Citation
三野星弥, 伴碧, 吉川雄一郎, 石黒浩. 非タスク指向型対話における話題の深さ推定モデルの構築. 言語処理学会第30回年次大会, 2024.
```
@InProceedings{Mitsuno_nlp2024,
  author = 	"三野星弥 and 伴碧 and 吉川雄一郎 and 石黒浩",
  title = 	"非タスク指向型対話における話題の深さ推定モデルの構築",
  booktitle = 	"言語処理学会第30回年次大会",
  year =	"2024"
}
```

## Acknowldegment
本研究はJSPS科研費 JP20H00101, JP19H05691, JP23KJ1462, Society 5.0 実現化研究拠点支援事業の助成を受けたものです．
