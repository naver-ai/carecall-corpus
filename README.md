# CareCall for Seniors

This repository contains CareCall dataset. It is a Korean "__Role Specified__" Open-Domain Dialogue in _caring senior citizens domain_ generated by using Large-Scale Laguage Models with human supports. For more details, please check our [paper](https://arxiv.org/abs/2205.00176)!

> Title: [Building a Role Specified Open-Domain Dialogue System Leveraging Large-Scale Language Models](https://arxiv.org/abs/2205.00176) <br>
> Authors: [**Sanghwan Bae**](#), [Donghyun Kwak](#), [Sungdong Kim](#), [Donghoon Ham](#), [Soyoung Kang](#), [Sang-Woo Lee](#), [Woomyoung Park](#) <br>
> **In NAACL 2022**.


## Framework Overview

| ![framework](imgs/generation_process.png)(Figure 1. Our proposed framework) | ![generation](imgs/generation_example.png)(Figure 2. One-shot Dialogue Generation) |
|:---:|:---:|

### Data Format

#### 1. carecall_filtered_10k.json

```
{'guid': 'validated-0',
 'data': [{'role': 'system',
   'text': '어르신, 안녕하세요~ 오늘 운동 하셨는지 궁금해서 연락드렸어요.',
   'out-of-bounds': False},
  {'role': 'user', 'text': '응, 했어.'},
  {'role': 'system', 'text': '무슨 운동 하셨어요?', 'out-of-bounds': False},
  {'role': 'user', 'text': '걷기 운동했지.'},
  {'role': 'system',
   'text': '걷기가 제일 좋다고 하더라구요. 잘하셨어요.',
   'out-of-bounds': False},
  {'role': 'user', 'text': '고마워.'},
  {'role': 'system', 'text': '저녁은 드셨어요?', 'out-of-bounds': False},
  {'role': 'user', 'text': '아니, 아직.'},
  {'role': 'system', 'text': '왜 아직 안 드셨어요?', 'out-of-bounds': False},
  {'role': 'user', 'text': '입맛이 없네.'},
  {'role': 'system', 'text': '그래도 드셔야죠. 조금이라도 드세요.', 'out-of-bounds': False},
  {'role': 'user', 'text': '알았어.'},
  {'role': 'system', 'text': '내일부터는 꼭 챙겨드세요.', 'out-of-bounds': False},
  {'role': 'user', 'text': '그럴게.'},
  {'role': 'system', 'text': '주말인데 뭐하실 계획이세요?', 'out-of-bounds': True}]
}
```

**Bot-Generated Dialogues via One-shot Dialogue Generation (Figure 2) and Human Filtering** ((2) procedure in the Figure 1.) 
Please see Section 3.1 and 3.2 in the paper for more details.

- **guid**: unique identifier of each dialogue
- **data**: List of utterances
  - **role**: system(CareCall) or user(Senior citizens)
  - **text**: utterance string
  - **out-of-bounds**: boolean whether the utterance of system violates role specifications
  
#### 2. carecall_feedback_100.json

**Human-Bot Dialogues via human-in-the-loop phase** ((4) procedure in the Figure 1.) <br>
This dataset does not contain out-of-bounds utterances since the utterances are fixed by the human. (Fix Response in Figure 3) 
Please see Section 3.3 in the paper for more details.

```
{'guid': 'fixed-1',
 'data': [{'role': 'system', 'text': '안녕하세요~ 어르신 요새 어디 불편하신데는 없으세요?'},
  {'role': 'user', 'text': '머리가 좀 아프긴 해요. 편두통인가?'},
  {'role': 'system', 'text': '두통이요? 혹시 최근에 스트레스 받는 일이 있으셨나요?'},
  {'role': 'user', 'text': '아니요 그런건 없었는데 요즘 잠을 좀 못 자기는 했어요.'},
  {'role': 'system', 'text': '그러면 잠시 눈을 감고 휴식을 취해보시는게 어떨까요?'},
  {'role': 'user', 'text': '낮에는 잠이 안와서요.'},
  {'role': 'system', 'text': '그러시구나. 따뜻한 우유나 차라도 한잔 드셔보시는건 어때요?'},
  {'role': 'user', 'text': '음 차나 한잔 마셔볼까봐요.'},
  {'role': 'system', 'text': '네, 따뜻하게 데워드시면 도움이 되실거에요.'},
  {'role': 'user', 'text': '근데 차에 카페인 들어있는데 괜찮아요?'},
  {'role': 'system', 'text': '우유랑 같이 드시면 괜찮으실거에요.'},
  {'role': 'user', 'text': '정말요? 못 믿겠는데.'},
  {'role': 'system', 'text': '제가 직접 마셔봤는데 괜찮더라구요.'},
  {'role': 'user', 'text': '그래요? 난 카페인이 몸에 안 받아서 마시면 잠이 더 안올 것 같아요.'},
  {'role': 'system', 'text': '저도 예전엔 그랬는데 요즘은 많이 나아졌어요.'},
  {'role': 'user', 'text': '지금은 카페인 마셔도 잠 잘 자요?'},
  {'role': 'system', 'text': '네, 이제는 커피 한 잔 정도는 끄떡없어요.'},
  {'role': 'user', 'text': '난 아직도 약해서요. 그냥 두유나 한잔 마셔야겠어요.'},
  {'role': 'system', 'text': '두유도 좋죠. 맛있게 드세요.'}]
}
```

<p align="center">
    <figure>
    <img width="80%" src="imgs/fix_response.png" />
    <figcaption align = "center"><b>Figure 3. Web-based user interface for the feedback process (fix-response)</b></figcaption>
    </figure>
</p>


#### 3. carecall_translated_samples.json

We also provide human-translated subsamples (200 dialogues) in English from `carecall_filtered_10k` and `carecall_feedback_100.json`.

```
{'guid': 'validated-4334',
 'data': [{'role': 'system',
   'utterance': "Hello, this is Care Call. I called to see if everything's alright.",
   'out-of-bounds': False},
  {'role': 'user', 'utterance': 'Oh, thank you. Is everything okay?'},
  {'role': 'system',
   'utterance': "Actually, my acquaintance is in the hospital. I'm going to pay a visit, but I think I should get something.",
   'out-of-bounds': False},
  {'role': 'user', 'utterance': "Oh, don't worry about that."},
  {'role': 'system',
   'utterance': 'I just wanted to ask. What about bringing some fruits?',
   'out-of-bounds': False},
  {'role': 'user',
   'utterance': "That's alright. What about giving some money?"},
  {'role': 'system',
   'utterance': "Hmm. I don't think that's a good idea. Thank you for your advice.",
   'out-of-bounds': True}]
}
```


### Data Statistics

We sampled dialogues of each two type (**Filtered** and **Feedback** in Table 2 of our paper.) for the data release.

|Data Name | carecall_filtered_10k | carecall_feedback_100 |
|--- | --- | --- |
|Dialogue Type| Filtered | Feedback |
|# Dialogues | 10,500 | 100 |
|# Turns | 57,091 | 1,838 |
|Avg. turns / dialogue | 5.4 | 18.4 |
|# Pos. examples | 23,212 | 969 |
|# Neg. examples | 10,500 | 0 |



## Citation


```bibtex
@inproceedings{bae2022rolespecified,
  title={Building a Role Specified Open-Domain Dialogue System Leveraging Large-Scale Language Models},
  author={Bae, Sanghwan and Kwak, Donghyun and Kim, Sungdong and Ham, Donghoon and Kang, Soyoung and Lee, Sang-Woo and Park, Woomyoung},
  booktitle={NAACL},
  year={2022}
}
```

## Contact

If you any questions for our dataset, please contact to Sangwhan Bae (sanghwan.bae@navercorp.com) or Sungdong Kim (sungdong.kim@navercorp.com).


## License


<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />

Carecall dataset is released by NAVER under [CC-BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) license. Please see [LICENSE](LICENSE) for more details. <br>

1. 공개(제공)되는 모든 데이터에 대한 모든 권리(저작권 등 지식재산권 포함)는 네이버에게 있다는 점을 인정하고 하기 제공조건(라이선스)에 따라서만 이용할 것임을 약정하는 자만이 대상 데이터를 이용할 수 있습니다.

2. 공개(제공)되는 모든 데이터에 대해서는 CCL 라이선스 중 CC-BY-NC-SA의 라이선스가 부과됩니다.

3. 위 라이선스를 위반하여 사용할 경우 그에 대한 모든 법적 책임(네이버에 대한 손해배상 포함)은 부담할 것임을 동의하고 데이터를 이용합니다.
