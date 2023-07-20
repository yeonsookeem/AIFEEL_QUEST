# AIFFEL Campus Online 5th Code Peer Review
- 코더 : 김민식 
- 리뷰어 : 김연수


# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네, 모두 정상적으로 동작하며, 주어진 과제에 맞는 결과가 도출되었습니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네, 주석이 상세히 적혀 있어서 전체적인 코드 이해에 도움이 되었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 모두 문제 없이 작동하는 것으로 보아, 에러를 유발할 코드는 없는 것으로 보입니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, 주석과 마크다운의 내용으로 보아 전체 코드에 대한 충분한 이해를 바탕으로 작성된 것 같습니다.
- [X] 코드가 간결한가요?
  > 네, 간결합니다.

# 개선 사항 제안 
> 없습니다.

# 잘 작성된 점
1) 주석이 상세히 적혀 있어서 전체적인 코드 이해에 도움이 되었습니다.
```python
# 데이터셋 다운로드 관련 정보 설정
file_name = 'ChatbotData.csv'
file_url = 'https://raw.githubusercontent.com/songys/Chatbot_data/master/ChatbotData.csv'
cache_subdir = 'data'
cache_dir = '/aiffel/aiffel/transformer_chatbot'

# 데이터셋 저장 여부를 파악할 파일 경로
## check_target_file_path값은 아래 주석과 같아진다.
### '/aiffel/aiffel/transformer_chatbot/data/ChatbotData_test.csv'
check_target_file_path = os.path.join(cache_dir, cache_subdir, file_name)

if os.path.isfile(check_target_file_path) == False:
    # 파일이 check_target_file_path에 없다면 데이터셋 다운로드
    path_to_csv = tf.keras.utils.get_file(fname=file_name, 
                                          origin=file_url, 
                                          extract=False, 
                                          cache_subdir = cache_subdir, 
                                          cache_dir=cache_dir)
    # 테스트 기준 노드의 심볼릭 링크로 완성된 파일명은 `ChatbotData .csv` 였다.
    print("데이터셋 다운로드 완료")
else:
    # 파일이 존재하면 이곳의 print()문이 수행된다.
    print("데이터셋 존재함. skip downloading..")
```

2) 한국어 데이터 전처리
```python
# 공백과 특수문자를 전처리하는 함수를 선언
def preprocess_sentence(sentence):
  # 입력받은 sentence를 소문자로 변경하고 양쪽 공백을 제거
  sentence = sentence.lower().strip()

  # 단어와 구두점(punctuation) 사이의 거리를 만듭니다.
  # 예를 들어서 "출석체크 하세요." => "출석체크 하세요 ."와 같이
  # '하세요'와 온점 사이에 거리를 만듭니다.
  sentence = re.sub(r"([?.!,])", r" \1 ", sentence)
  sentence = re.sub(r'[" "]+', " ", sentence)

  # 한글, 영어, 숫자, "?", "!", "."를 제외한 모든 문자를 공백인  '로 대체합니다.
  # 참고: https://signing.tistory.com/74
  sentence = re.sub(r"[^a-zA-Z0-9가-힣?.!,]+", " ", sentence)
  sentence = sentence.strip()
  return sentence
```

3) 프로젝트 후, 회고까지 잘 이루어졌습니다.

학습을 10회만 수행해서 그런지, 답변이 어색한 경우도 있었다. 그리고 특정 표현(레스고)에 대해 단어 사전이 정의되어 있지 않아, 답변이 이상하게 느껴지는 경우도 있었다. 추후 학습을 늘려서 수행해보거나, 단어 사전을 좀 더 심도있게 구성하여 테스트를 해보면 좀 더 그럴듯한 챗봇이 되지 않을까 생각한다.
