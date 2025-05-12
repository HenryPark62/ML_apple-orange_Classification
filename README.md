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
| **Baseline CNN** | - 간단한 Conv2D + MaxPooling 기반 CNN | - 정확도는 나쁘지 않지만 오분류 케이스 비율이 낮지 않음<br>- Test 정확률 약 89% |
| **강화 Baseline CNN** | - Baseline CNN + Data Augmentation | - 정확도 향상<br>- Test 정확률 약 94% |
| **VGG-Style CNN** | - Data Augmentation 적용<br>- Label Smoothing 적용<br>- ReduceLROnPlateau 적용 | - VGG 모델 스타일로 정교하게 구현<br>- 정확도 향상<br>- Test 정확률 약 95% |

---

## 📊 Research Summary

* Baseline CNN → Baseline CNN + Data Augmentation → Label Smoothing & Learning Rate Scheduler 적용 VGG style CNN 
* 최종 결과: **VGG style CNN (model_v5)** (Test 정확률 약 95%)
* 소량 데이터에서는 Fine-Tuning의 필요성이 크게 느껴지지 않음
* Label Smoothing, ReduceLROnPlateau 적용으로 일반화 성능 강화

---

## 📊 ROC Curve, Confusion Matrix, Classification Report


* **ROC Curve**
![1756baac-d510-4c2f-b9e7-4596972338b4](https://github.com/user-attachments/assets/98d1fbfe-13c7-46db-8c3e-446ca84ce5f5)

* AUC (Area Under Curve): 약 0.96

* **Confusion Matrix (model_v5 (VGG style))**

![a1ccd89b-e834-4691-a616-d97567cb0b12](https://github.com/user-attachments/assets/e2d90cae-860c-4169-9c0f-c504edff593b)



* **Classification Report**

<img width="553" alt="스크린샷 2025-05-12 오후 10 13 25" src="https://github.com/user-attachments/assets/4b9bf396-7648-4acc-82fe-3883e2301a4b" />



* Binary Classification

![6949e362-4bd5-40b1-9986-b60f94474e31](https://github.com/user-attachments/assets/62206bfa-ef72-46ee-ab01-b4bbf95ad7bd)

![8ef78b66-7909-4440-afe2-cfe6bb37fa06](https://github.com/user-attachments/assets/4c522814-6939-4570-97da-c5a3e9162613)

---

## 📊 결론 (Baseline CNN vs 최적화 CNN vs MobileNetV2)

* **Baseline CNN**
  * 빠른 학습 가능
  * Overfitting 심각

* **VGG-Style 강화 CNN**
  * Regularization 적용 및 깊은 레이어 구조로 Test 성능 향상

* **MobileNetV2 (전이학습)**
  * 경량화 + 전이학습 효과로 가장 우수한 성능 확보

---

## 💡 Insight

* Label Smoothing + Learning Rate Scheduler를 통한 일반화 성능 강화
* Fine-Tuning은 소량 데이터에서는 신중한 조정이 필요
* Data Augmentation은 unseen 데이터 대응력 향상에 효과적
* Confusion Matrix를 통해 정/오분류 사례를 검토하고 필요한 추가 데이터 수집 방향을 설정할 수 있음

---
