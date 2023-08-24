# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김민식
- 리뷰어 : 황인준


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [x] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 훈련 중에 에러가 발생해서 번역 성능은 확인 할 수 없었습니다. 하지만 전체적인 흐름은 맞았습니다.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네 주석이 이해가 필요한 곳에 적절히 배치되어있었습니다.
- [x] 코드가 에러를 유발할 가능성이 없나요?
  > 회고에서 밝혔듯이 OOM문제가 발생했다. batch size나 dimension의 조정이 필요할 수 있다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네 작성자는 프로젝트의 방향성을 이해하고 작성했습니다.
- [O] 코드가 간결한가요?
  > 네 코드가 간결하게 구성되어있습니다.
  


# 참고 링크 및 코드 개선
 ```python
BATCH_SIZE     = 32
SRC_VOCAB_SIZE = len(enc_tokenizer.index_word) + 1
TGT_VOCAB_SIZE = len(dec_tokenizer.index_word) + 1

units         = 1024
embedding_dim = 512

encoder = Encoder(SRC_VOCAB_SIZE, embedding_dim, units)
decoder = Decoder(TGT_VOCAB_SIZE, embedding_dim, units)

# sample input
sequence_len = 30
```
units나 embedding_dim이 너무 커서 oom문제가 발생했을수 있어서 작은 차원부터 복잡도를 높여가며 확인해보는것도 좋을것 같습니다.

 ```python
# 한글 문장 전처리 함수 선언
def preprocess_ko_sentence(sentence, s_token=False, e_token=False):
    sentence = sentence.lower().strip()

    sentence = re.sub(r"([?.!,])", r" \1 ", sentence)
    sentence = re.sub(r'[" "]+', " ", sentence)
    sentence = re.sub(r"[^ㄱ-ㅎㅏ-ㅣ가-힣]+", " ", sentence)

    sentence = sentence.strip()

    if s_token:
        sentence = '<start> ' + sentence

    if e_token:
        sentence += ' <end>'
    
    return sentence

print("preprocess_ko_sentence() 선언 완료!")
```
저희가 사용한 한국어 corpus에 영어가 섞인 경우도 있는것 같아서 영어도 같이 전처리해주거나 아니면 영어가 포함된 corpus를 지워주는 과정이 있어도 좋을것 같습니다.
