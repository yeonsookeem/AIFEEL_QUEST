# AIFFEL Campus Online 5th Code Peer Review
- 코더 : 김민식
- 리뷰어 : 박혜원


# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 평가 기준

    얼굴 영역과 랜드마크를 정확하게 검출하고, 스티커 사진을 합성시키는 데 성공하였다. (O)
    정확한 좌표계산을 통해 고양이 수염의 위치가 원본 얼굴에 잘 어울리게 출력되었다. (O)
    얼굴각도, 이미지 밝기, 촬영거리 등 다양한 변수에 따른 영향도를 보고서에 체계적으로 분석하였다. (△)
    - "추가로 생각해볼만한 부분" 에 이 부분에 대한 고찰은 담겨있었지만, 조금 더 구체적으로 분석 과정이 제시 되었으면 좋았을 것 같습니다. 

- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 주석을 상세하게 달아주셔서 이해하기 쉬웠습니다. 
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 실행 해본 결과 모두 오류없이 작동하는것을 확인했습니다
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네 상세한 주석과, 노드 학습 기반의 내용으로 작성된 것을 확인 할 수 있었습니다. 
- [O] 코드가 간결한가요?
  > 네 특히 고양이 수염 스티커를 코 중심점에 맞추는 과정을 간단 명료하게 작성해주셨다고 생각합니다. 

# 개선 사항 제안 
- "추가로 생각해볼만한 부분" 에서 추측하신 것처럼, 위 face detector 는 각도에 따라 잘 detect 를 못하기도 하는데, 반측면 얼굴은 detect 를 합니다. 반측면 얼굴에 대해서 고양이 스티커를 적용시키는 Case 에 대해서도 적용해보시기를 제안드립니다. 

아래는 스티커 위치를 변형시키는 함수의 예시 코드입니다. 

```python
# 스티커 변형 위치 파악
def sticker_transformation_test(image):
    image_show = image.copy()   # 원본 이미지 image_show 이름으로 저장
    detector_hog = dlib.get_frontal_face_detector() # Face detector, Returns the default face detector
    dlib_rects = detector_hog(image, 1)             # detect input img, para 1 means 1 times upsamle

    # detected 얼굴 시각화
    for rect in dlib_rects:
        left = rect.left()      # left x value
        top = rect.top()        # top y value
        right = rect.right()    # right x value
        bottom = rect.bottom()  # detect box bottom y value

        # add detect box in image
        cv2.rectangle(image_show, (left, top), (right, bottom), (0,255,0), 2) # 상자 그리기 Face Detection

    list_landmarks = []

    # 얼굴 영역 박스 마다 face landmark를 찾아냄.
    for dlib_rect in dlib_rects:
        landmark_predictor = dlib.shape_predictor("/content/shape_predictor_68_face_landmarks.dat")
        points = landmark_predictor(image_show, dlib_rect)
        list_points = list(map(lambda p: (p.x, p.y), points.parts())) # face landmark 좌표를 저장
        list_landmarks.append(list_points)  # total 68 landmark count

    # landmark 출력
    for landmark in list_landmarks:
        for point in landmark:
            cv2.circle(image_show, point, 2, (0, 128, 255), -1)

    # 고양이 스티커의 영역(꼭지점으로 연결)
    vertices1 = np.array([landmark[1], landmark[29], landmark[33], landmark[3]])
    vertices2 = np.array([landmark[29], landmark[15], landmark[13], landmark[33]])
    cv2.polylines(image_show, [vertices1], isClosed=True, color=(0, 128, 255))
    cv2.polylines(image_show, [vertices2], isClosed=True, color=(0, 128, 255))

    plt.imshow(cv2.cvtColor(image_show, cv2.COLOR_BGR2RGB))
    plt.show()

```


