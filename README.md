# Visual Semantic Reasoning for Image-Text Matching (VSRN)
PyTorch code for VSRN described in the paper "Visual Semantic Reasoning for Image-Text Matching". The paper will appear in ICCV 2019 as oral presentation. It is built on top of the [VSE++](https://github.com/fartashf/vsepp).

[Kunpeng Li](https://kunpengli1994.github.io/), [Yulun Zhang](http://yulunzhang.com/), [Kai Li](http://kailigo.github.io/), Yuanyuan Li and [Yun Fu](http://www1.ece.neu.edu/~yunfu/). "Visual Semantic Reasoning for Image-Text Matching", ICCV, 2019. [[pdf](https://arxiv.org/pdf/1909.02701.pdf)]

## Introduction
Image-text matching has been a hot research topic bridging the vision and language areas. It remains challenging because the current representation of image usually lacks global semantic concepts as in its corresponding text caption. To address this issue, we propose a simple and interpretable reasoning model to generate visual representation that captures key objects and semantic concepts of a scene. Specifically, we first build up connections between image regions and perform reasoning with Graph Convolutional Networks to generate features with semantic relationships. Then, we propose to use the gate and memory mechanism to perform global semantic reasoning on these relationship-enhanced features, select the discriminative information and gradually generate the representation for the whole scene. Experiments validate that our method achieves a new state-of-the-art for the image-text matching on MS-COCO and Flickr30K datasets. It outperforms the current best method by 6.8\% relatively for image retrieval and 4.8\% relatively for caption retrieval on MS-COCO (Recall@1 using 1K test set). On Flickr30K, our model improves image retrieval by 12.6\% relatively and caption retrieval by 5.8\% relatively (Recall@1).

![model](/fig/model.png)

## Requirements 
We recommended the following dependencies.

* Python 2.7 
* [PyTorch](http://pytorch.org/) (0.4.1)
* [NumPy](http://www.numpy.org/) (>1.12.1)
* [TensorBoard](https://github.com/TeamHG-Memex/tensorboard_logger)
* [pycocotools](https://github.com/cocodataset/cocoapi)
* [torchvision]()
* [matplotlib]()


* Punkt Sentence Tokenizer:
```python
import nltk
nltk.download()
> d punkt
```

## Download data

Download the dataset files and pre-trained models. We use splits produced by [Andrej Karpathy](http://cs.stanford.edu/people/karpathy/deepimagesent/). 

We follow [bottom-up attention model](https://github.com/peteanderson80/bottom-up-attention) and [SCAN](https://github.com/kuanghuei/SCAN) to obtain image features for fair comparison. More details about data pre-processing (optional) can be found [here](https://github.com/kuanghuei/SCAN/blob/master/README.md#data-pre-processing-optional). All the data needed for reproducing the experiments in the paper, including image features and vocabularies, can be downloaded from [SCAN](https://github.com/kuanghuei/SCAN) by using:

```bash
wget https://scanproject.blob.core.windows.net/scan-data/data.zip
```

You can also get the data from google drive: https://drive.google.com/drive/u/1/folders/1os1Kr7HeTbh8FajBNegW8rjJf6GIhFqC. We refer to the path of extracted files for `data.zip` as `$DATA_PATH`. 

## Training new models
Run `train.py`:

For MSCOCO:

```bash
python train.py --data_path $DATA_PATH --data_name coco_precomp --logger_name runs/coco_VSRN --max_violation
```

For Flickr30K:

```bash
python train.py --data_path $DATA_PATH --data_name f30k_precomp --logger_name runs/filker_VSRN --max_violation --max_len 40
```

## Evaluate trained models
Modify the model_path and data_path in the evaluation_models.py file. Then Run `evaluation_models.py`:

```bash
python evaluation_models.py
```

To do cross-validation on MSCOCO 1K test set, pass `fold5=True`. Pass `fold5=False` for evaluation on MSCOCO 5K test set. Pretrained models can be downloaded from https://drive.google.com/file/d/1C4Z8ZgJuvrChigPO7g-IGd68y6VqWQ5n/view?usp=sharing


## Reference

If you found this code useful, please cite the following paper:

    @inproceedings{li2019vsrn,
      title={Visual semantic reasoning for image-text matching},
      author={Li, Kunpeng and Zhang, Yulun and Li, Kai and Li, Yuanyuan and Fu, Yun},
      booktitle={ICCV},
      year={2019}
    }

## License

[Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)


