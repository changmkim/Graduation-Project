# Video retrieval, captioning 기반 동영상 필터링 모델
## Summary
본 연구에서는 수집된 비디오 데이터의 설명문을 생성하고, 이를 비디오의 text feature로 활용하여 retrieval을 진행한다. 이때, text feature와 비디오 간의 유사도를 이용하여 관련 없는 비디오를 필터링하는 모델을 구현한다. MSR-VTT 데이터셋에 대해 이 방법을 적용한 후 군집화를 통해 비디오를 필터링한 결과, 유사한 비디오는 captioning 모델에 의해 비슷하거나 동일한 설명문을 생성하기 때문에 같은 군집에 속하는 경향이 있고, 영상에 대한 명확한 설명문을 생성하지 못한 경우 비슷한 동영상임에도 다른 군집으로 분류된다. 

## Built with
* [sklearn](https://scikit-learn.org/stable/)
* [retrieval model](https://openaccess.thecvf.com/content/CVPR2022/papers/Shvetsova_Everything_at_Once_-_Multi-Modal_Fusion_Transformer_for_Video_Retrieval_CVPR_2022_paper.pdf)
* [captioning model](https://openaccess.thecvf.com/content/CVPR2022/papers/Ye_Hierarchical_Modular_Network_for_Video_Captioning_CVPR_2022_paper.pdf)

## Project description
### 프로젝트 시나리오
<img src="https://github.com/changmkim/Graduation-Project/assets/73116458/052bef5a-34d2-4054-a3d1-b50d3a709cb1" width="100%">

1) captioning 모델, retrieval 모델을 수행하기 위한 동영상 feature 추출
2) 추출된 동영상 특성으로 captioning 모델을 이용해 설명문 생성
3) 생성된 설명문을 동영상의 text feature로 세팅
4) retrieval 모델 동작
5) 각 동영상에 대한 텍스트 특성(생성된 설명문)에 대한 비디오 특성(프레임 별 이미지) 사이의 코사인 유사도 추출
6) 추출한 동영상간의 유사도를 이용해 군집화

### 이미지간의 유사도 상관관계 및 산점도
<img src="https://github.com/changmkim/Graduation-Project/assets/73116458/f03b6531-78cc-4483-ba4c-48cb1df353ca" width="100%">

## Result
### 군집화 결과
#### DBSCAN 사용 결과
- 기존 20개 군집을 유지한 데이터셋에 대하여 총 30개 군집, 79개의 이상치 데이터 검출
  
#### DBSCAN 군집2
![image](https://github.com/changmkim/Graduation-Project/assets/73116458/ef150afe-3e21-4ba4-9442-188fc1d3a1d5)

#### 분석
- 유사한 동영상의 경우 유사한 설명문 생성으로 생성된 텍스트가 다른 동영상을 비슷하게 검색하는 경향을 보임
- 군집화의 경우 패러미터의 조정, 설명문 생성 모델 성능 개선으로 더 정밀한 효과를 보일 것으로 예상
- retrieval 모델의 영향은 적은 편
