# *When did you become so smart, oh wise one?!* Sarcasm Explanation in Multi-modal Multi-party Dialogues

This repository contains the code required to reproduce the results of our ACL 2022 paper - "*When did you become so smart, oh wise one?!* Sarcasm Explanation in Multi-modal Multi-party Dialogues".

The paper introduces the novel task of sarcasm explanation in dialogues (SED). Set in a multimodal and code-mixed setting, the task aims to generate natural language explanations of satirical conversations.
An example case is illustrated in the figure below:

![SED Example](/imgs/se_eg4-1.png)

It contains a dyadic conversation of four utterances hu1, u2, u3, u4i, where the last utterance (u4) is a sarcastic remark. Note that in this example,
although the opposite of what is being said is, “I don’t have to think about it," it is not what the speaker means; thus,
it enforces our hypothesis that sarcasm explanation goes beyond simply negating the dialogue’s language.
The discourse is also accompanied by ancillary audio-visual markers of satire such as an ironical intonation of the pitch, a blank face, or roll of the eyes.
Thus, conglomerating the conversationhistory, multimodal signals, and speaker information, SED aims to generate a coherent and cohesive natural language
explanation associated with these sarcastic dialogues.

We augment [MaSaC](https://github.com/LCS2-IIITD/MSH-COMICS), a multi-modal, code-mixed, sarcasm detection dataset in dialogues with code-mixed explanations to create **WITS** (**W**hy **I**s **T**his **S**arcastic?) dataset.

### Data Format
##### Text Features: JSON
```
{
  'd_id': {
    'episode_name': title,
    'target_speaker': speaker1,
    'target_utterance': t_utt,
    'context_speakers': [sp_a, ..., sp_b],
    'context_utterances': [utt_a, ..., utt_b],
    'code_mixed_explanation': cmt_exp,
    'sarcasm_target': t_sp,
    'start_time': start_time,
    'end_time': end_time
    }
  ...
}
```

##### Audio Features: DataFrame
```
| episode_name	| target_speaker | target_utterance | context_speakers | context_utterances | sarcasm_target | code_mixed_explanation | start_time | end_time | audio_feats |
```

##### Video features: DataFrame
```
| episode_name	| target_speaker | target_utterance | context_speakers | context_utterances | sarcasm_target | code_mixed_explanation | start_time | end_time | video_feats |
```

### Training and Evaluation
- Download data features from [this drive link](https://drive.google.com/drive/folders/1hUnoicZPwCWB0IZfZ3X28-vc58O-saXt?usp=sharing).
- Place the text, audio, and video feature files in the format as described above in the following manner in the 'Data' folder:
    - Data
        - Text
            - train_text.json
            - val_text.json
            - test_text.json
        - Audio
            - train_audio.p
            - val_audio.p
            - test_audio.p
        - Video
            - train_video.p
            - val_video.p
            - test_video.p
- Execution
    - Go to the 'Code' directory and run ```python Trimodal-BART-driver.py```.

Models will be saved in the 'models' directory while generated explanations on the val and test sets will be saved in the 'results' folder.
