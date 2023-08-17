`mskim_init.ipynb`
> 과제 시간 안에 작성한 내역을 업로드함

`mskim_ps_test.ipynb`
> 추가로 인지한 부분을 보강하여 내역을 업로드하는 코드

---

# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김민식
- 리뷰어 : 김연수


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네, 모두 정상적으로 동작한 것으로 보입니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 주석이 매우 자세하게 적혀있어서, 코드 이해에 도움이 되었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 없이 잘 작동하는 것으로 보입니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, 부족한 부분은 추가로 업데이트 해서 올리신 것으로 보아, 코드에 대한 충분한 이해가 바탕이 된 것 같습니다.
- [X] 코드가 간결한가요?
  > 네, 간결합니다.

# 예시
```python
ef sp_train(model_type=None):
    # 불용어 설정
    ## 참고1: https://github.com/google/sentencepiece/blob/master/doc/special_symbols.md?plain=1
    ## 참고2: https://wikidocs.net/44249
    stopwords = ['의','가','이','은','들','는','좀','잘','걍','과','도','를','으로','자','에','와','한','하다']
    ## stopwords 값들을 하나의 문장으로 엮음
    stopwords_sen = ','.join(stopwords)
    ## 명령어 옵션 추가, 불용어
    commanderize = ''.join(['--user_defined_symbols=', stopwords_sen])
    
    ## 초기 명령어 샘플
    init_command = '--input={} --model_prefix=korean_spm --model_type=unigram --vocab_size={} --minloglevel={}'
    
    ## 적용할 명령어, default is 'unigram'
    command = ' '.join([init_command, commanderize])
    
    ### --input={} --model_prefix=korean_spm --model_type=unigram --vocab_size={} 
    ### --minloglevel={}
    ### --user_defined_symbols=의,가,이,은,들,는,좀,잘,걍,과,도,를,으로,자,에,와,한,하다
    
    ## minloglevel 값, 단어 빈도수 조절, 입력된 값 미만인 단어는 무시함
    word_frequency = 2
    
    if model_type == 'bpe':
        command = command.replace('--model_type=unigram', '--model_type=bpe')
```
- 모델을 RNN, 1D CNN, GlobalMaxPooling1D의 다양한 방법으로 구성하고 평가했습니다.
- 그래프 시각화가 많이 되어있어, 이해하는데 큰 도움이 되었습니다.
- 전반적으로 실험과 테스트, 리뷰가 잘 되어있습니다.

# 참고 링크 및 코드 개선

