# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 김민식
- 리뷰어 : 손정민


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 주석이 상세하게 적혀 있어 의도를 알기 쉬웠고 코드의 진행을 파악하는 데에 도움이 되었습니다.
  ```python
  ## 1. 나이브 베이즈 정확도
  predicted = model.predict(tfidfv_test) #테스트 데이터에 대한 예측
  print("정확도:", accuracy_score(y_test, predicted)) #예측값과 실제값 비교
  ## 2. CNB 정확도
  predicted = cb.predict(tfidfv_test) #테스트 데이터에 대한 예측
  print("정확도:", accuracy_score(y_test, predicted)) #예측값과 실제값 비교
  ## 3. 로지스틱 회귀 정확도
  predicted = lr.predict(tfidfv_test) #테스트 데이터에 대한 예측
  print("정확도:", accuracy_score(y_test, predicted)) #예측값과 실제값 비교
  ```
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 메시지 출력된 부분에 주석으로 설명해주셨고, 나머지 부분은 에러 없이 잘 실행되었습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 주석이나 회고 내용으로 보아 프로젝트에 대해 잘 이해하고 과제를 수행한 것으로 보입니다.
- [X] 코드가 간결한가요?
  > 변수명이 직관적이고 코드 간 개행이 적절하여 가독성이 좋았습니다.


# 참고 링크 및 코드 개선
 개선할 부분은 따로 보이지 않습니다. 수행 과정마다 회고가 있는 게 인상깊었습니다. 한 과정을 본 직후에 회고를 통해 의도나 추가적인 생각을 알 수 있어 좋았습니다.
