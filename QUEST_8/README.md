# AIFFEL Campus Online 5th Code Peer Review
- 코더 : 김민식 
- 리뷰어 : 최연석


# PRT(PeerReviewTemplate)
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 수행 항목에 알맞게 수정하였습니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 각 함수별 주석이 있어 이해하기 쉬웠습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 오류가 발생한 부분은 없으며 해당 데이터셋으로 빌드시 오류 발생 가능성이 없어 보입니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 전처리, 모델설계, 생성, 평가등 순차에 맞게 작성 하였습니다.
- [X] 코드가 간결한가요?
  > 네 class 및 함수화 하여 작성 하였습니다.

# 학습된 모델로 결과 Input Image / Predicted Image / Ground Truth 출력
```
# 이미지 denormalize하여 확인하기
for val_image in os.listdir(val_path):
    f = os.path.join(val_path, val_image)
    input_image, real_image = load_img(f)

    pred = generator(tf.expand_dims(input_image, 0))
    pred = denormalize(pred)

    plt.figure(figsize=(20,10))
    plt.subplot(1,3,1); plt.imshow(denormalize(input_image)); plt.title('Input Image', fontsize=15)
    plt.subplot(1,3,2); plt.imshow(pred[0]); plt.title('Predicted Image', fontsize=20)
    plt.subplot(1,3,3); plt.imshow(denormalize(real_image)); plt.title('Ground Truth', fontsize=15)
```
# 학습과 loss 출력 확인
```
# 10 epoch의 학습 진행
EPOCHS = 10

generator = UNetGenerator()
discriminator = Discriminator()
history = {'gen_loss':[], 'l1_loss':[], 'disc_loss':[]} # loss 값 시각화를 위해 생성

for epoch in range(1, EPOCHS+1):
    for i, (sketch, colored) in enumerate(train_images):
        g_loss, l1_loss, d_loss = train_step(sketch, colored)
        history['gen_loss'].append(g_loss)
        history['l1_loss'].append(l1_loss)
        history['disc_loss'].append(d_loss)      
            
            
        # 10회 반복마다 손실을 출력합니다.
        if (i+1) % 10 == 0:
            print(f"EPOCH[{epoch}] - STEP[{i+1}] \
                    \nGenerator_loss:{g_loss.numpy():.4f} \
                    \nL1_loss:{l1_loss.numpy():.4f} \
                    \nDiscriminator_loss:{d_loss.numpy():.4f}", end="\n\n")
```

# 개선 사항 제안 
