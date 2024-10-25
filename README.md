# 의료 데이터의 멀티 모달 학습을 기반으로 한 임상 기록 생성 모델 
Clinical Note Generation Model Based on Multimodal Learning of Medical Data

## 🔨코딩기록
24/10/25 5PM: 일단 참고했던 깃허브 코드로도 돌아가기는 하는데, 마찬가지로 성능이 좋지 않은 걸 보아서는 이미지와 텍스트 데이터셋에 문제가 있지 않을까 싶음 (깃허브 참고한데에서는 잘 돌아가는걸 보면...) -> 일단 깃허브 코드 기준으로 데이터셋 한번 수정해보고, 여기서 되면 기존 clip projection 코드에도 그 결과 적용해보기 - 가능하다면!
<br>✔️ 이후에 ref-git 코드 기준으로 어디서부터 잘못되었는지 확인해보기

24/10/26 1AM: 참고했던 깃허브의 트랜스포머 인퍼런스 보니까 beam search를 사용했길래 이 코드도 포함해서 test를 작성했는데 여기서 문제가 발생하는것같은데 어떻게 해결해야할지 잘 모르겠다.

**<오류 발생 코드>**
```python
outputs = t5_model(
                encoder_outputs=encoder_outputs.repeat(beam_size, 1, 1),
                decoder_input_ids=decoder_input_ids,
                return_dict=True
            )
```

이 부분에서 Not enough values to unpack (expected 3, got 2) 오류가 발생하는데 텐서 크기도 맞춰봐도 정답이 안 나온다... 혹시 테스트에서는 정답 텍스트 없이 t5_model을 구동해야 해서 values가 없다고 하는건지...

## ❓질문할 것
- clip-projection.ipynb는 내가 작성한 코드인데 아예 생성 자체가 랜덤(?)인지 제대로 생성되지 않고, 나머지 노트북 파일은 참고했던 깃허브에 내가 가지고 있는 데이터를 적용한 것인데 얘도 제대로 생성되지 않는데 코드 리딩 부탁드리기
- 사실 전자 코드는 어디가 잘못되서 생성이 안 되는건지 모르겠다
- 만약 후자 코드 쓸거라면 여기서 왜 위의 오류가 발생하는지...
