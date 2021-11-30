# 2021 Computer Vision Term Project
4개 분야 선정하여 베이스라인 찍기
## My Repository
1. [2D Objection Detection](https://github.com/JYEDU/CV_YOLOv5)
2. [Scene Text Recognition](https://github.com/JYEDU/CV_Scene_Text_Recognition)
3. [Super Resolution](https://github.com/JYEDU/CV_Super_Resolution)
4. [Image to Image(Ther2RGB)](https://github.com/JYEDU/CV_Image-To-Image)

<br/><br/>
# Scene Text Recognition (ViSTR)

1. Challenge Leaderboard

    - [LINK](http://203.250.148.129:3088/web/challenges/challenge-page/32/overview)




2. Scene Text Recognition 챌린지 개요

    - Otical Character Recognition(OCR) 작업 중 하나 <br/>
    - 컴퓨터가 물체의 레이블, 도로 표지판 등과 같은 natural scene에 존재하는 텍스트를 읽을 수 있게 함  <br/>
    - machine이 어떤 방향으로 가는지 어떤 행동을 취할지, 어떤 물체를 선택할 지와 같은 텍스트 정보에 기반할 결정을 내릴 수 있도록 도와줌

<br/>

![image](https://user-images.githubusercontent.com/87462769/143524872-d7c378ad-0881-42e7-b877-f6a0c30b719f.png)

<br/>   

3. 방법론 (ViTSTR-Tiny)

    - 한 단계로 구성된 가장 단순한 아키텍처를 가지고 있음
    - 이미지를 여러 개의 patches로 나누고, Linear Projection을 통해 1D vector patch embedding으로 변환 
    - patch embedding은 position encoding과 합한 후 Transformer Encoder의 입력으로 들어가 예측된 character sequence를 출력함

<br/>

![image](https://user-images.githubusercontent.com/87462769/143813016-b8c9844f-9ebb-4b10-bc78-0f7a48524511.png)

<br/>   

4. 데이터셋

    - lmdb 파일로 저장된 데이터 사용
    - train dataset : MJ-ST
    - test dataset : Regular Dataset (IIIT5K, SVT, IC03, IC13)
                     Irregular Dataset (IC15, SVTP, CT)
                     

5. 참고자료
    - [[Paper](https://arxiv.org/abs/2105.08582)] Vision Transformer for Fast and Efficient Scene Text Recognition
    - [[Paper](https://arxiv.org/abs/1904.01906)] What Is Wrong With Scene Text Recognition Model Comparisons? Dataset and Model Analysis
    - [[Github](https://github.com/roatienza/deep-text-recognition-benchmark)] ViTSTR GitHub Repository
    - [[Github](https://github.com/Denny-Warhol/2021ComputerVision-Scene-Text-Recognition)] 2021ComputerVision-Scene-Text-Recognition Repository
    - [[Youtube](https://www.youtube.com/watch?v=1CBn6AmTa2w&list=PL1xKqHsVFgvnM3zhBkbTZy5l_13x5R3Jq&index=5)] 2021 Computer Vision - Scene Text Recognition

<br/><br/><br/><br/>
 
## 원복 과정에 대한 챌린지 제출 파일
### ① eval.ai 리더보드상의 기록 캡쳐본
![image](https://user-images.githubusercontent.com/87462769/143812324-b08c7796-a444-45cb-8346-72d0f30bca6b.png)
### ② 베이스라인을 찍기 위한 나의 repository
[[Github](https://github.com/JYEDU/CV_Scene_Text_Recognition)]
### ③ 제출 과정에 대한 동영상 링크(베이스라인 알고리즘 설명 및 베이스라인을 찍기 위한 과정을 설명)
[[Youtube](https://youtu.be/0vTweVWWDuc)]



<br/><br/>

## 원복 코드
```
# git clone
git clone https://github.com/roatienza/deep-text-recognition-benchmark.git

# download the file named dataset2.py and predict.py to get the result file
git clone https://github.com/Denny-Warhol/2021ComputerVision-Scene-Text-Recognition.git

# change directory
cd deep-text-recognition-benchmark

# install library
pip3 install –r requirements.txt

# train
python train.py --train_data data_lmdb_release/training --valid data data_lmdb_release/evaluation –select_data MJ-ST --batch_ratio 0.5-0.5 --Transformation None --FeatureExtraction None --SequenceModeling None --Prediction None --Transformer --TransformerModel=vistr_tiny_patch16_224 --imgH 224 --imgW 224 --manualSeed=0 –sensitive 

# test
python predict.py --eval_data data_lmdb_release/evaluation --benchmark_all_eval --Transformation None --FeatureExtraction None --SequenceModeling None --Prediction None --Transformer --TransformerModel=vistr_tiny_patch16_224 -–sensitive --data_filtering_off --imgH 224 --imgW 224
```

