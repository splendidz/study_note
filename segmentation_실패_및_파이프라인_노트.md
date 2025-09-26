# Failure Note

- **YOLOv8 Segmentation** 모델 자체 학습 실패  
  (PNG 마스크 등 데이터 전처리 문제는 없었는데도 성능 불안정)
- **U-Net 구현 Segmentation 시도**  
  - 공개 웹 dataset에서는 성능 양호
  - 그러나 **도메인 조금만 달라지면(예: 다른 직소 퍼즐 이미지)** → 정확도 급격히 하락
- **이미지 전처리 필요성** 강하게 느낌

---

# 파이프라인 구상

- **YOLO Object Detection**: bbox 검출 (예: color 기반)

### 실제 예시 파이프라인
```
[입력 이미지] 
    ↓
[YOLO] → 자동차 bbox 검출
    ↓
[자동차 crop 이미지]
    ↓
[Segmentation Model (ex: mini-UNet, DeepLab)]
    ↓
[세부 segmentation 결과 (mask)]
```

---

# Insight

- **U-Net이 처음엔 좋아보였던 이유**
  - Kaggle 등 튜토리얼 데이터셋은 매우 정제되고 제한된 환경
  - 따라서 초반에는 성능이 잘 나와서 “모든 segmentation이 가능하다”는 착각을 주기 쉬움

- **현실 환경은 훨씬 복잡**
  - 다양한 조명, 각도, 카메라 품질, 노이즈, 배경 변화 등 변수 존재
  - 한 가지 모델만으로는 범용적 성능 확보 어려움

### ✅ 결론
- “한방에 해결” 모델은 거의 없음
- **Detection + Segmentation + 전처리 조합**이 핵심
- 데이터 다양성 확보와 전처리 전략이 정확도를 크게 좌우