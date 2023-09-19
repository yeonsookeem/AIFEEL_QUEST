# AIFFEL Campus Online Code Peer Review 
- 코더 : 김민식
- 리뷰어 : 김연수


# PRT(Peer Review Template)
- [ ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    -  모든 문제를 해결한 것은 아니지만, 주어진 task 모두 실행하기 위해 노력하신 것으로 보입니다.
  ```python
  #데이터 전처리 후, 평가 결과 비교
  #BLUE SCORE
    import nltk
    from nltk.translate.bleu_score import sentence_bleu

    def bleu_score(reference, candidate):
        # 실제 번역된 문장 (모델의 출력)
        reference = reference.split()
    
    # 모델이 생성한 번역 후보 문장
    candidate = candidate.split()
    
    # BLUE 스코어 계산
    bleu_score = sentence_bleu([reference], candidate)
    
    # 소수점 이하 4자리까지 출력
    formatted_bleu_score = format(bleu_score, '.4f')
    
    return formatted_bleu_score

   #ROUGE SCORE
    from rouge_score import rouge_scorer

    def rough_socre_n1(reference, candidate):
    
    ## ROUGE 스코어 계산; ROUGE-1 (1-gram)
    score_1 = rouge_scorer.RougeScorer(['rouge1'])
    scores_1 = score_1.score(reference, candidate)
    
    

    return scores_1

    def rough_socre_n2(reference, candidate):
    ## ROUGE 스코어 계산; ROUGE-2 (2-gram)
    score_2 = rouge_scorer.RougeScorer(['rouge2'])
    scores_2 = score_2.score(reference, candidate)

    return scores_2
  ```
  ```python
  #모델 교체
  # 모델 선언
    model_name = 'EleutherAI/LLaMA'
    model = AutoModelForCausalLM.from_pretrained(model_name)
    tokenizer = AutoTokenizer.from_pretrained(
    model_name, bos_token='</s>', eos_token='</s>', unk_token='</s>', pad_token='</s>',
    padding_side="right",
    model_max_length=512,
    )

    print(tokenizer)
  ```
    
- [X]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
  주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 네, 주석이 꼼꼼하게 잘 작성돼있었고,코드 자체의 가독성 또한 좋습니다.
    ```python
    # SFT 데이터셋 전처리 함수 생성
    ## completion의 길이를 체크하여 특정 길이 이상의 데이터를 없애는 로직으로 접근
    def check_sentence_length(list_dict, MAX_LEN=250):
    res_list = []
    
    for item in list_dict:
        if len(item['completion']) <= MAX_LEN:
            res_list.append(item)
    
    return res_list
    ```
    - 도식을 잘 활용하셔서, 전체적인 코드 이해에 도움이 되었습니다.
      ```python
        # 통계적 요약 정보
        summary_stats = df.describe()
        print(summary_stats)
        ```
- [X]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
  ”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 네, 에러 코드가 존재하며, 이를 해결하기 위해 추가 학습중이신 것으로 보입니다.
     
      
- [X]  **4. 회고를 잘 작성했나요?**
    - 네, 마지막에 루브릭이 작성돼있습니다.
      
- [X]  **5. 코드가 간결하고 효율적인가요?**
    - 효율적입니다.
  ```python
  # PRO 학습에 사용할 데이터 불러와 토크나이징
    with open('/aiffel/KoChatGPT/data_kochatgpt/kochatgpt_3_PPO.jsonl', "r", encoding='utf-8-sig') as json_file:
     list_data_dict = json.load(json_file)
     list_prompt = [tmp['prompt'] for tmp in list_data_dict]

    def tokenize_fn(texts):
     batch = tokenizer(texts, return_tensors='pt', max_length=96, padding=True, truncation=True)
     return {k: v.cuda() for k, v in batch.items()}
    ```
    

# 참고 링크 및 코드 개선
```
-
```
