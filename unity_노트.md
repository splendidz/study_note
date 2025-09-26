# Unity의 세 가지 주요 파이프라인

## Built-in Render Pipeline (기본, 전통적인 방식)
- Unity 초창기부터 있던 기본 파이프라인.
- 많은 예전 튜토리얼들이 이걸 기반으로 함.
- 단순하고 호환성이 넓음.
- 대신 최적화나 커스터마이즈가 제한적임.

## URP (Universal Render Pipeline)
- 모바일, PC, 콘솔까지 범용으로 쓸 수 있게 만든 현대식 파이프라인.
- 성능과 효율에 맞게 설계됨.
- Shader나 머티리얼이 Built-in과 다름. (예: `_Color` 대신 `_BaseColor`)
- 요즘 Unity에서 기본으로 추천하는 파이프라인.

## HDRP (High Definition Render Pipeline)
- 고사양 PC, 차세대 콘솔, 영화 같은 퀄리티를 목표로 함.
- 물리 기반 조명, 사실적인 반사/굴절 표현.
- 초보자보다는 고급 그래픽 프로젝트용.

---

## 왜 중요할까?
파이프라인에 따라 **머티리얼, 셰이더, 조명 시스템**이 다르기 때문에,
프로젝트를 처음 만들 때 파이프라인을 잘못 고르면 →
튜토리얼 코드/재질이 안 맞아서 **핑크 화면** 같은 문제가 생깁니다.

### ✅ 정리
- Unity에서 "파이프라인"이란 **렌더링 절차**예요.
- Built-in, URP, HDRP 중 **하나를 프로젝트 단위로 선택**해야 하고, 그 선택에 따라 사용할 **머티리얼/셰이더/스크립트 코드**도 달라집니다.

---

# 핵심 뼈대(필수 개념)
- **GameObject**: "껍데기" 그 자체. 모든 것은 게임오브젝트.
- **Component**: 기능을 붙이는 "부품". 예) Transform, MeshRenderer, Collider, Script 등.
- **Transform**: 위치/회전/크기. 모든 GameObject에 1개씩.
- **Prefab**: 오브젝트의 "설계도(템플릿)". 복제/재사용 용이, Variant로 일부만 바꾸기 가능.
- **Scene**: 현재 작업 중인 "무대(지도 한 장)". 여러 씬을 로딩/전환 가능.

---

# 렌더(보여주는) 라인
- **Mesh**: 점·선·면으로 만든 3D 형태(큐브, 구, 로봇팔 등).
- **MeshRenderer**: Mesh를 화면에 "그려주는" 컴포넌트.
- **Material(머티리얼)**: "겉옷". 색/질감/광택/반사 같은 시각 속성 묶음.
- **Shader(셰이더)**: 머티리얼이 **어떻게** 그려질지 GPU에 알려주는 "프로그램".
  - Built-in: **Standard**
  - URP: **Universal Render Pipeline/Lit**
  - **핑크 화면** = 현재 파이프라인에서 그 셰이더를 못 씀.
- **Texture(텍스처)**: 이미지 파일. 색(Albedo/BaseMap), 거칠기, 법선 등 다양한 맵으로 사용.
  - **Base Map(Albedo)**: 기본 색/무늬.
  - **Normal Map**: 울퉁불퉁한 표면 느낌.
  - **Metallic/Smoothness**: 금속성/매끈함. (URP는 마스크 조합 방식이 다를 수 있음)
- **UV**: 텍스처를 메시에 "어디에 어떻게" 붙일지 좌표.
- **Tiling/Offset**: 텍스처 반복/이동 값.

---

# 파이프라인(렌더 파이프라인)
- **Built-in**: 오래된 기본 방식. 예전 튜토리얼 호환 좋음.
- **URP**: 최신 범용. 성능/기능 밸런스 좋아 **산업/로봇 시뮬 추천**.
- **HDRP**: 초고사양·포토리얼. 전시/홍보 영상용에 적합.
- **Render Pipeline Asset**: 프로젝트가 어떤 파이프라인을 쓸지 지정하는 설정 에셋.
- **Shader Graph**: 코딩 없이 노드로 셰이더 제작.
- **Renderer Feature(URP)**: 커스텀 후처리/윤곽선/디버그 패스 추가.

---

# 카메라·조명·후처리
- **Camera**: 화면에 담는 눈.
  - **FOV(시야각)**, **Clipping Planes(가시 거리)**, **Clear Flags(배경 처리)**
  - **Perspective/Orthographic(원근/직교)**
- **Light**: 방향(Directional)/점(Point)/스팟(Spot)/영역(Area, HDRP). 그림자 품질/성능 트레이드오프.
- **GI/Lightmap**: 정적인 조명/그림자를 미리 굽는 베이킹(성능↑).
- **Reflection Probe**: 반사 표현을 위한 환경 캡처.
- **Post-processing(후처리)**: Bloom/Color Grading/DOF 등.
  - Built-in: **PPSv2** / URP·HDRP: **Volume 시스템**

---

# 물리(Physics)
- **Rigidbody**: 물리 시뮬 대상(질량/중력/관성).
  - **Use Gravity**, **Constraints**, **Interpolation**, **Collision Detection(Discrete/Continuous)**
- **Collider**: 충돌 모양(박스/구/캡슐/메시). **Is Trigger**면 통과 이벤트만.
- **Physic Material**: 마찰/탄성.
- **Update vs FixedUpdate**:
  - **FixedUpdate** = 물리 프레임(기본 0.02s). 힘/속도 적용은 여기에.
  - **Update** = 화면 프레임. 입력/로직.
- **Time.deltaTime**: 프레임 간 시간. 이동에 곱해서 속도 일정 유지.
- **Layers & Collision Matrix**: 어떤 레이어끼리 충돌할지 설정.

---

# 애니메이션/네비
- **Animator**: 상태머신으로 애니메이션 전환.
- **Animation Clip**: 애니메이션 데이터.
- **Root Motion**: 애니가 이동을 주도할지 여부.
- **NavMesh / NavMeshAgent**: 길찾기(경로 계획).
- **NavMeshObstacle**: 장애물.

---

# 스크립팅(코드)
- **MonoBehaviour**: 유니티 컴포넌트 기반 스크립트의 부모 타입.
- **Awake / OnEnable / Start**: 초기화 타이밍(참조 연결/런타임 세팅).
- **Update / LateUpdate / FixedUpdate**: 매 프레임 / 렌더 후 / 물리 프레임.
- **Coroutine**: `IEnumerator` + `yield`로 비동기 흐름.
- **Instantiate / Destroy**: 생성/파괴.
- **DontDestroyOnLoad**: 씬 전환 시 유지.
- **Script Execution Order**: 스크립트 호출 순서 지정.
- **Input System**:
  - **Old**: `Input.GetAxis` / `Input.GetKey`
  - **New(Input System)**: 액션/바인딩 기반. 프로젝트 세팅과 코드가 맞아야 오류 없음.

---

# UI
- **Canvas**: UI를 그리는 공간.
  - **Screen Space - Overlay/Camera**, **World Space**
- **RectTransform**: UI 전용 Transform(앵커/피벗/레이아웃).
- **EventSystem**: 클릭/터치 이벤트 처리.
- **Canvas Scaler**: 해상도 대응.
- **UGUI vs UI Toolkit**: 전통 UI(UGUI)와 최신(에디터·툴링 친화적) UI.

---

# 에셋/프로젝트 관리
- **Assets 폴더**: 모든 리소스의 실제 저장 위치(버전관리 중요).
- **Import Settings**: 텍스처/모델/오디오의 가져오기 옵션(Read/Write, sRGB, Compression, Mip Map).
- **Resources 폴더**: 런타임 로드용(남발 금지, Addressables 권장).
- **Addressables**: 대규모 프로젝트의 에셋 로딩/버전/메모리 관리 솔루션.
- **Package Manager**: URP/HDRP/Input System 등 기능 패키지 관리.

---

# 2D 전용(필요 시)
- **Sprite / SpriteRenderer**: 2D 이미지/렌더러.
- **Sorting Layer / Order in Layer**: 그려지는 앞뒤 순서(3D의 Z와 별개).
- **Tilemap**: 격자 기반 맵 제작.
- **2D Physics(Box2D)**: Rigidbody2D / Collider2D / Joint2D / Gravity Scale.

---

# 성능·최적화 키워드
- **Draw Call**: 그리기 호출 수(적을수록 좋음).
- **Batching**: 호출 묶기. **Static/Dynamic Batching**, **SRP Batcher(URP)**.
- **GPU Instancing**: 같은 메시에 **색만 다른** 다량 렌더에 유리.
- **Culling**: **Frustum/Backface/Occlusion**로 보이지 않는 건 스킵.
- **LOD Group**: 거리별 저해상도 메시로 교체.
- **MaterialPropertyBlock**: 머티리얼 공유 유지하면서 **개별 색/값**만 바꿀 때 사용(배치에 유리).
- **sharedMaterial vs material**:
  - `sharedMaterial` 바꾸면 **모든 오브젝트에 영향**.
  - `material`은 인스턴스 복제(개별 변경, GC 비용 유의).

---

# 입문자가 자주 겪는 함정(빠른 해결집)
- **모두 핑크**: 파이프라인과 셰이더가 불일치(URP 프로젝트에서 Standard 사용 등).
  - → URP 머티리얼로 업그레이드 또는 Graphics Settings의 SRP Asset 제거.
- **색이 전부 동시에 바뀜**: `sharedMaterial`을 바꿈.
  - → `renderer.material` 또는 **MaterialPropertyBlock** 사용.
- **물리 튀거나 느슨**: 힘/속도는 **FixedUpdate**에서, 이동은 **deltaTime** 고려.
- **레이어 충돌 과다**: Layer Collision Matrix로 불필요한 충돌 끄기.
- **캔버스 UI가 흐릿/크기 이상**: Canvas Scaler 설정 확인(Reference Resolution / Scale with Screen Size).
- **Z-Fighting**: 같은 평면이 겹침 → Z 오프셋/두께/거리 조정.

---

# 로봇/산업 시뮬 팁(바로 활용)
- **스케일 관례**: 1 유니티 단위 ≈ 1미터(일관성 유지가 관건).
- **물리 시간**: Project Settings → Time → **Fixed Timestep**(물리 해상도). 0.02s 기본.
- **카메라**: **Orthographic** 카메라는 도면/톱뷰 UI에 유용.
- **렌더**: URP + SRP Batcher + Instancing으로 대량 오브젝트 렌더.
- **색상 개별화**: 대량 큐브/팔레트 표시 = **MaterialPropertyBlock** 패턴 고정.
- **디버그용 Gizmos**: 에디터 뷰에서 경로/작업영역/충돌 반경 시각화.

---

# 아주 짧은 예시: 큐브 색을 개별로(URP/Built-in 겸용)
```csharp
var mr = GetComponent<MeshRenderer>();
var mpb = new MaterialPropertyBlock();
mr.GetPropertyBlock(mpb);
if (mr.sharedMaterial != null && mr.sharedMaterial.HasProperty("_BaseColor"))
    mpb.SetColor("_BaseColor", myColor); // URP/HDRP
else
    mpb.SetColor("_Color", myColor);     // Built-in
mr.SetPropertyBlock(mpb);
```

