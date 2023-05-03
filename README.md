# SpeechBSD corpus

This is an extension of the [BSD corpus](https://github.com/tsuruoka-lab/BSD) with audio files and speaker attribute information.

## Download

```
git clone https://github.com/ku-nlp/speechBSD.git
cd speechBSD
wget https://lotus.kuee.kyoto-u.ac.jp/~sshimizu/data/speechBSD_wav_20221026.tar.gz
tar zxvf speechBSD_wav_20221026.tar.gz
```

## Statistics

|           |  Train |  Dev. |  Test |
| --------- | ------:| -----:| -----:|
| Scenarios |    670 |    69 |    69 |
| Sentences | 20,000 | 2,051 | 2,120 |
| En audio (h) | 20.1 | 2.1 | 2.1 |
| Ja audio (h) | 25.3 | 2.7 | 2.7 |
| En audio gender (male % / female %) | 47.2 / 52.8 | 50.1 / 49.9 | 44.4 / 55.6 |
| Ja audio gender (male % / female %) | 68.0 / 32.0 | 62.3 / 37.7 | 69.0 / 31.0 |

## Structure

- `wav` directory contains wav files (16 kHz, mono channel), which are classified to `train`, `dev`, and `test`.
- `txt` directory contains json files split to `train`, `dev`, and `test`.
	- Each json file is a list of scenarios.
	- Each scenario contains:
		- `id`, `tag`, `title`, and `original_language`, which are identical to the ones of the BSD corpus, and `conversation`
	- `conversation` is a list of utterances. Each utterance contains:
		- `no`, `ja_speaker`, `en_speaker`, `ja_sentence`, `en_sentence` that are identical to the ones of the BSD corpus
		- `ja_spkid` and `en_spkid` that show speaker IDs consistent throughout the conversation
		- `ja_wav` and `en_wav` that show the wavfile names located in the `wav` diretory
		- `ja_spk_gender` and `en_spk_gender` that show the gender of the speaker of the corresponding wav file
		- `ja_spk_prefecture` and `en_spk_state` that show where the speaker come from

```
[
    {
        "id": "190315_E001_17",
        "tag": "training",
        "title": "Training: How to do research",
        "original_language": "en",
        "conversation": [
            {
                "no": 1,
                "en_speaker": "Mr. Ben Sherman",
                "ja_speaker": "ベン シャーマンさん",
                "en_sentence": "I will be teaching you how to conduct research today.",
                "ja_sentence": "今日は調査の進め方についてトレーニングします。",
                "ja_spkid": "190315_E001_17_spk0_ja",
                "en_spkid": "190315_E001_17_spk0_en",
                "ja_wav": "190315_E001_17_spk0_no1_ja.wav",
                "en_wav": "190315_E001_17_spk0_no1_en.wav",
                "ja_spk_gender": "M",
                "en_spk_gender": "M",
                "ja_spk_prefecture": "大阪",
                "en_spk_state": "CA"
            },

```


### Notes

- Gender is one of "M" or "F".

- Speakers are different if speaker ID is different.
  For example, if a conversation is spoken by two speakers taking turns, there would be 4 speakers (2 Japanese speakers and 2 English speakers).
  However, it's possible that speakers with different speaker ID is actually spoken by the same person because of the way audio is collected.

- Gender information of audio does not necessarily match with the one inferrable from text.
  For example, even if the `en_speaker` is "Mr. Sam Lee", the audio may contain female voice.
  This is because no explicit gender information is given in the original BSD corpus.

- Japanese speech is collected from Japanese speakers who are from Japan.
	- `ja_spk_prefecture` is one of the 47 prefectures or "不明" (unknown).
		- Prefectures that ends with "県" or "府" does not contain those characters (e.g., "神奈川", "京都").
		- Tokyo is "東京" without "都".
		- Hokkaido is "北海道".

- English speech is collected from English speakers who are from the US.
	- `en_spk` is one of the 50 states, written in postal abbreviation.


## License

This dataset is licensed under [CC-BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
