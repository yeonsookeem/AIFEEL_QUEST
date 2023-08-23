# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김민식
- 리뷰어 : 손정민


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [ ] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 정상적으로 동작하지만 전체 장르에 대한 편향성을 구하는 부분이 없었습니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 주석이 자세하게 달려있고 마크다운을 이용한 설명이 함께 있어 이해하기 쉬웠습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 없이 잘 실행되었습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 주석의 내용, 노드를 변형한 코드로 보아 사용한 방법에 대해 잘 이해하고 작성한 것으로 보입니다.
  ```python
  ...
  # 대표 단어와 유사한 단어 10개 출력
    ## 하면서 target_1 (X) 에 append
    print(f"{target_word}과 관련 있는 상위 10개 단어들:")
    for word, similarity in similar_words:
        # target or attribute
        target_or_attribute_list.append(similarity)
        print(f"{word}: {similarity:.4f}")
  ...
  ```
- [X] 코드가 간결한가요?
  > 반복되는 코드는 함수로 표현하였고 적절한 개행을 사용하여 가독성이 좋았습니다. 변수명 또한 직관적인 이름으로 알아보기 쉬웠습니다.
  ```python
  # Word2Vec 부분이 반복적이므로 함수 선언
  def w2v_model(nouns, target_word, target_or_attribute_list):
      # 모델 학습 - 명사 단어 기반
      model = Word2Vec([nouns], vector_size=100, window=5, min_count=1, sg=0, workers=4)

      # 대표 단어 - 단어 뭉치 기준 관련성이 높은 10개 단어 추출
      similar_words = model.wv.most_similar(positive=target_word, topn=10)
      ...
    
  ```


# 참고 링크 및 코드 개선
 프로젝트 노드에서 제공한 장르명 리스트를 이용해 전체 장르별 예술/일반 영화에 대한 편향성을 구하고 시각화하는 과정이 추가되면 좋을 것 같습니다.