# WSL에서 Qt 관련 에러 발생 시 해결 방법

## 에러 메시지 예시
```
qt.qpa.plugin: Could not load the Qt platform plugin "xcb" in "" even though it was found.
This application failed to start because no Qt platform plugin could be initialized.
Reinstalling the application may fix this problem.

Available platform plugins are: eglfs, linuxfb, minimal, minimalegl, offscreen, vnc,
wayland-egl, wayland, wayland-xcomposite-egl, wayland-xcomposite-glx, webgl, xcb.
```

## 원인
- Qt 기반의 GUI 라이브러리(PyQt, PySide, matplotlib, OpenCV `cv2.imshow()` 등)를 사용하는 프로그램이 **디스플레이 환경이 없는 서버/WSL/headless 환경**에서 실행될 때 자주 발생.
- 특히 `xcb` 플러그인을 로드하지 못하면 GUI 창을 띄우려다 실패하고 프로그램이 종료됨.

## 해결 방법

### 1. Ubuntu (WSL 포함)에서 패키지 설치
```bash
sudo apt update
sudo apt install libxcb-xinerama0
```

### 2. Conda 환경에 Qt 관련 패키지 추가
```bash
conda install pyqt
# 또는
conda install qt
```

---

## 추가 팁
- GUI 기능이 필요 없는 경우(서버 실행 등): matplotlib를 non-GUI 백엔드로 설정
  ```python
  import matplotlib
  matplotlib.use('Agg')  # PNG 등 파일로 저장만 함, 창 띄우지 않음
  ```
- OpenCV 사용 시 GUI가 필요 없다면 `cv2.imshow()` 대신 `cv2.imwrite()`로 파일 저장.
- 원격 GUI가 꼭 필요하다면 **X11 Forwarding**(예: `ssh -X`) 또는 **VcXsrv** 같은 Windows X Server를 설치 후 연동 가능.

