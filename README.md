# ᓀ‸ᓂ Fidget Companion "FidgetPal"

> `pdgt-companion` is typo. :P

# Release
[FidgetPal](https://fidget-companion.vercel.app)

## Korean

### 주의사항
- 본 앱은 책상 등 고정 장소에 놓고 쓰는 것을 전제로 값이 설정되어 있으므로, 스마트폰 등 손에 들고 사용하는 환경에서는 매우 민감하게 동작할 수 있습니다.
- 컴패니언의 격렬한 반응을 보기 위해 기기를 **절대 세게 내리치거나 강한 충격을 주지 마십쇼.**
- **위 주의사항을 어길 시 발생하는 모든 기기 파손 및 고장에 대한 책임은 전적으로 본인에게 있습니다.**

### 핵심 취지
본 프로젝트는 모바일 브라우저의 물리 센서 데이터를 제어하는 실험적 웹앱입니다. 요소를 화면에서 숨기면 헨더링을 비활성화하는 Safari WebKit 엔진의 정책을 ViewPort 내 투명화와 무한 렌더링 루프를 통해 우회하였습니다.

[개발 취지 보기(한국어)](https://blog.naver.com/scope-hyena/224332346363)

### 로컬 실행 방법
1. 저장소를 클론하고 프로젝트 폴더로 이동합니다.
```bash
git clone https://github.com/codestudy-484c/pdgt-companion
cd pdgt-companion
```
2. 의존성 라이브러리를 설치합니다.
```bash
npm install
```
3. 로컬 개발 서버를 실행합니다. (`--host` 옵션으로 모바일 로컬 접속을 테스트할 수 있슴다)
```bash
npm run dev -- --host
# 또는 npx vite --host
```

### 기기별 실행 및 활용 방법
#### iPhone
Safari 브라우저로 접속해 🔌 버튼을 눌러 가속도 센서 권한을 부여한 뒤, 📺 버튼을 눌러 PIP 모드로 전환합니다. 브라우저를 내리고 타 앱을 사용해도 PIP 플레이어 내에서 컴패니언이 가속도 센서의 값을 읽고 반응합니다.

#### iPad
Safari로 접속하여 [공유] 버튼을 눌러 [홈 화면에 추가]를 눌러 웹앱으로 설치합니다. '윈도우 모드' 실행 상태에서 Slide Over로 설치된 웹앱을 실행하고 🔌 버튼을 눌러 가속도 센서 권한을 부여한 뒤, 적당한 크기로 조정하여 사용합니다. (하단 컨트롤 버튼은 자동으로 숨겨지며 앱 화면 터치 시 다시 표시됩니다)

## English

### Precautions
- This app is calibrated for use on a stable, fixed surface like a desk. Therefore, it may behave highly sensitively when used while holding it in your hand (e.g., on a smartphone).
- **DO NOT** slam or apply strong impacts to your device just to see a violent reaction from the companion.
- **You are solely responsible for any device damage or malfunction caused by violating the warnings above.**

### Core Purpose
This project is an experimental web app designed to control and map physical sensor data from mobile browsers. It bypasses the Safari WebKit engine's optimization policy—which automatically disables rendering when elements are hidden from the screen—by utilizing in-viewport transparency and an infinite rendering loop.

[View Development Purpose (Korean)](https://blog.naver.com/scope-hyena/224332346363)

### Local Setup & Execution
1. Clone the repository and navigate into the project folder.
```bash
git clone https://github.com/codestudy-484c/pdgt-companion
cd pdgt-companion
```
2. Install required dependencies.
```bash
npm install
```
3. Run the local development server (You can testthemobile local connection using the `--host` option.)
```bash
npm run dev -- --host
# or npx vite --host
```

### Usage by Device
#### iPhone
1. Access the app via Safari browser.
2. Tap the 🔌 button to grant accelerometer permissions.
3. Tap the 📺 button to switch PiP mode.
   > **NOTE**
   > if you minimize the browser to the background and use other apps, the companion will continue to read the accelerometer values and react smoothly within the native PiP player

#### iPad
1. Access the app via Safari, tap the [Share] button, and select [Add to Home Screen] to install it as a web app.
2. While using your iPad in Window mode, launch the installed web app as a Slide Over window.
3. Tap the 🔌 button to grant accelerometer permissions, and resize the window to your preference.
   > **NOTE**
   > The bottom control buttons will automatically slide down and hide to keep the focus entirely on the companion, and will reappear instantly when you tap the screen.
