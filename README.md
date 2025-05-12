# 🍎🍊 딥러닝 기반 사과 & 오렌지 분류 모델 (Apple & Orange Binary Classification using Deep Learning (VGG-Style CNN)

---

## 📌 프로젝트 개요

* **주제**: 사과와 오렌지 사진을 기반으로 과일 종류를 이진 분류
* **목표**: 경량 CNN 모델을 활용해 넓은 일반화 성능을 가진 분류기 개발 (Test Accuracy 95% 이상)

---

## 👤 데이터셋

* **데이터 출처**: kaggle 수집 (Apple / Orange 사진) (https://www.kaggle.com/datasets/kipshidze/apple-vs-orange-binary-classification)
* **구성**:
  * 기존 데이터셋은 Apple, Orange 사진으로만 구성되어 있어서 임의로 Train, Validation, Test 분리.
  * Train: 약 640장
  * Validation: 약 160장
  * Test: 약 80장
* **구성 방법**:
  * Train/Validation/Test 비율 조정 (80%, 10%, 10%)
  * 데이터 비율 고려하여 분할

---

## 🧪 모델 구조, 튜닝 및 연구

| 버전 | 주요 특징 | 결과 요약 |
|:----|:---------|:--------|
| **Baseline CNN** | - 간단한 Conv2D + MaxPooling 기반 CNN | - 정확도는 나쁘지 않지만 오분류 케이스 비율이 낮지 않음<br>- Test Accuracy 약 89% |
| **강화 Baseline CNN** | - Baseline CNN + Data Augmentation | - 정확도 향상<br>- Test Accuracy 약 94% |
| **VGG-Style CNN** | - Data Augmentation 적용<br>- Label Smoothing 적용<br>- ReduceLROnPlateau 적용 | - VGG 모델 스타일로 정교하게 구현<br>- 정확도 향상<br>- Test Accuracy 약 95% |

---

## 📊 Research Summary

* Baseline CNN → Baseline CNN + Data Augmentation → Label Smoothing & Learning Rate Scheduler 적용 VGG style CNN 
* 최종 결과: **VGG style CNN (model_v5)** (Test 정확률 약 95%)
* 소량 데이터에서는 Fine-Tuning의 필요성이 크게 느껴지지 않음
* Label Smoothing, ReduceLROnPlateau 적용으로 일반화 성능 강화

---

## 📊 ROC Curve, Confusion Matrix, Classification Report

**Baseline CNN**<br>

![163381e4-ee1c-441a-954e-7e8aa5115e1d](https://github.com/user-attachments/assets/db1441c7-9580-4bd8-a050-5555c6585c35)
![94c4242f-f0d0-43af-8a14-427653a26de9](https://github.com/user-attachments/assets/1ab71585-2739-44ad-b3e2-94b2ffb44f17)
<img width="539" alt="스크린샷 2025-05-12 오후 11 57 13" src="https://github.com/user-attachments/assets/ae8ccbf9-abc6-4791-823a-4e300971ee98" /><br>


**Baseline CNN + Data Augmentation**<br>

![4654f381-e0f8-4c1c-8258-dec0ceed738c](https://github.com/user-attachments/assets/48a18da8-86e9-45b4-8b85-884557ba62d3)
![6a841c34-aabd-4bb8-b624-d53d1f75134e](https://github.com/user-attachments/assets/daa7c362-f74d-4fee-a622-75bf04004e06)
<img width="539" alt="스크린샷 2025-05-12 오후 11 57 50" src="https://github.com/user-attachments/assets/a3f8bbfa-d353-409e-8230-4a4b0c2af7bb" /><br>


###**VGG-Style CNN**<br>
![cd0d8e64-ab47-4aad-b08d-c4de63316ba8](https://github.com/user-attachments/assets/643894e4-25b5-4eec-9a90-ed5735b24ced)
![a1ccd89b-e834-4691-a616-d97567cb0b12](https://github.com/user-attachments/assets/e2d90cae-860c-4169-9c0f-c504edff593b)
<img width="553" alt="스크린샷 2025-05-12 오후 10 13 25" src="https://github.com/user-attachments/assets/4b9bf396-7648-4acc-82fe-3883e2301a4b" />
![1756baac-d510-4c2f-b9e7-4596972338b4](https://github.com/user-attachments/assets/98d1fbfe-13c7-46db-8c3e-446ca84ce5f5)<br>




###**Binary Classification**<br>

![6949e362-4bd5-40b1-9986-b60f94474e31](https://github.com/user-attachments/assets/62206bfa-ef72-46ee-ab01-b4bbf95ad7bd)

![8ef78b66-7909-4440-afe2-cfe6bb37fa06](https://github.com/user-attachments/assets/4c522814-6939-4570-97da-c5a3e9162613)

---

## 📊 결론 (Baseline CNN vs 강화 Baseline CNN vs VGG-Style CNN)

* **Baseline CNN**
  * 빠른 학습 가능
  * 정확도가 아쉬움

* **강화 Baseline CNN** 
  * Data Augmentation을 통해 이미 높은 수준의 성능 향상 (Test Accuracy 약 94%)
  * 소량 데이터에서는 다른 모델보다 비교적 경량의 Baseline 모델을 사용해도 무리가 없을 것 같음

* **VGG-Style CNN**
  * Data Augmentation, Label Smoothing, ReduceLROnPlateau 적용을 통해 모델 성능의 향상, 학습 효율의 향상을 보임

---

## 💡 Insight

* Label Smoothing + Learning Rate Scheduler를 통한 학습 효율 및 일반화 성능 강화
* Fine-Tuning은 소량 데이터에서는 신중한 조정이 필요 (소량 데이터에서는 Fine-Tuning보단 Data Augmentation이 더 좋아보인다)
* Data Augmentation은 unseen 데이터 (Test data) 대응력 향상에 효과적
* Confusion Matrix를 통해 정/오분류 사례를 검토하고 필요한 추가 데이터 수집 방향을 설정할 수 있음

---
