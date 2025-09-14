# 🏆 AI 휴지통 종이 던지기 (Paper Toss AI)

이 프로젝트는 **강화학습(PPO, Stable-Baselines3)**을 활용하여 `휴지통 종이 던지기` 게임을 학습시키고, 학습된 모델을 **ONNX 형식으로 변환**하여 **웹 브라우저에서 실행 가능한 게임**으로 배포하는 것을 목표로 합니다.  

---

## 📌 프로젝트 개요
- **게임 환경:** Pygame 기반 종이 뭉치 던지기 게임
- **강화학습:** PPO 알고리즘으로 학습 (Stable-Baselines3)
- **모델 변환:** 학습된 SB3 모델을 ONNX로 변환
- **웹 실행:** onnxruntime-web을 이용해 브라우저에서 AI 플레이 시연
- **산출물:** 코드 저장소, 학습 로그, 그래프, 모델 파일, 시연 영상

---

## 📂 프로젝트 구조
```
├── environment.py       # Pygame 기반 Gymnasium 환경 정의
├── game.py              # 사람 플레이어용 Pygame 게임
├── train.py             # PPO 학습 스크립트
├── convert_onnx.py      # SB3 모델 → ONNX 변환 스크립트
├── model.onnx           # 변환된 최종 모델
├── final_model.zip      # 학습 완료된 Stable Baselines3 모델
├── index.html           # ONNX 모델을 불러와 실행되는 웹 게임
```

---

## ⚙️ 환경 설정

### 1. Python 환경
```bash
# 가상환경 생성
conda create -n papertoss python=3.10 -y
conda activate papertoss

# 필수 패키지 설치
pip install pygame gymnasium stable-baselines3 torch onnx onnxruntime
```

### 2. 추가 패키지 (옵션)
```bash
pip install tensorboard
```
→ 학습 로그 시각화에 필요

---

## 🚀 실행 방법

### 1. 학습 (Training)
```bash
python train.py
```
- `tensorboard_logs/` → 학습 로그 기록 (TensorBoard 실행 가능)
- `checkpoints/` → 주기적 체크포인트 저장
- 최종 학습 모델: `final_model.zip`

TensorBoard 실행:
```bash
tensorboard --logdir ./tensorboard_logs
```

---

### 2. ONNX 변환
```bash
python convert_onnx.py
```
- 입력: `final_model.zip`  
- 출력: `model.onnx`  
- 변환 과정에서 샘플 입력을 넣어 모델 검증 수행

---

### 3. 게임 실행
#### (1) Pygame에서 직접 플레이
```bash
python game.py
```

#### (2) 웹에서 AI 플레이 시연
```bash
# 로컬 서버 실행
python -m http.server 8080
```
→ 브라우저에서 [http://localhost:8080/index.html](http://localhost:8080/index.html) 접속  
→ 학습된 AI가 휴지통에 종이를 던지는 모습을 확인 가능

---

## 📊 결과 요약
- **학습 결과:**  
  PPO 알고리즘으로 약 100만 스텝 학습 후, AI는 다양한 조건(장애물, 바람)에서도 일정 성공률로 휴지통에 공을 넣음  
- **보상 곡선:**  
  초기에는 낮은 보상이지만 학습이 진행됨에 따라 평균 보상이 안정적으로 상승  
- **웹 시뮬레이션:**  
  학습된 모델이 ONNX로 변환되어 브라우저에서 실시간 실행 가능  
- **제출 산출물:**  
  - 코드 저장소 (환경, 학습, 변환, 실행)  
  - 학습 로그 및 보상 그래프  
  - 최종 모델 (`final_model.zip`, `model.onnx`)  
  - 시연 영상 또는 GIF (20~60초)  
  - 요약 보고서 (1–2쪽)  

---

## 🙌 배운 점
- **환경 설계의 중요성:** 관측/행동/보상 정의가 학습 성능을 크게 좌우  
- **PPO 알고리즘:** 안정적이고 비교적 빠른 학습을 보여줌  
- **배포 경험:** 강화학습 모델을 ONNX로 변환 후 웹에서 실행하는 엔드 투 엔드 파이프라인 구축 경험  
- **시각화:** TensorBoard 및 시연 영상을 통한 학습 과정/결과 확인  
