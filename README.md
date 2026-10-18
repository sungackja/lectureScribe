<p align="center">
  <img src="assets/lecturescribe-hero.png" alt="LectureScribe — 헤드폰을 쓴 민트색 녹음 도우미와 노트북" width="100%">
</p>

<h1 align="center">강의는 듣고, 기록은 맡겨요 🎧</h1>

<p align="center">
  강의 영상과 음성을 내 PC에서 녹취하고,<br>
  나만의 문서와 자막으로 정리하는 작은 공부 도우미.
</p>

<p align="center">
  <strong>🪟 Windows</strong> &nbsp; · &nbsp;
  <strong>🌿 로컬 전사</strong> &nbsp; · &nbsp;
  <strong>⚡ NVIDIA GPU</strong> &nbsp; · &nbsp;
  <strong>📦 v0.3.0</strong>
</p>

<p align="center">
  <a href="#-작은-도우미가-하는-일">기능 둘러보기</a> &nbsp; / &nbsp;
  <a href="#-세-걸음이면-완성">사용 방법</a> &nbsp; / &nbsp;
  <a href="#-얼마나-빠를까요">성능 기록</a> &nbsp; / &nbsp;
  <a href="docs/GUIDE.md">자세한 안내</a>
</p>

<p align="center">
  <a href="https://github.com/sungackja/lectureScribe/releases/latest/download/LectureScribe-Setup.exe"><strong>⬇️ Windows 설치 파일 다운로드 · v0.3.0</strong></a>
  &nbsp; · &nbsp;
  <a href="https://github.com/sungackja/lectureScribe/releases/latest">변경 사항 보기</a>
</p>

---

## 🌱 작은 도우미가 하는 일

<table>
<tr>
<td width="33%" valign="top">
<h3>🎬 파일을 툭</h3>
<p>MP4 · MP3 · WAV · M4A · MKV를 끌어놓아요. 여러 강의도 대기열에서 차례로 처리해요.</p>
</td>
<td width="33%" valign="top">
<h3>🎧 내 PC에서 녹취</h3>
<p>Whisper와 Qwen 모델이 NVIDIA GPU로 음성을 글로 바꿔요. 강의를 전사 API에 보내지 않아요.</p>
</td>
<td width="33%" valign="top">
<h3>📝 나만의 기록으로</h3>
<p>문장을 검색하고 수정해요. TXT · Word · 자막으로 저장하고, 원본도 함께 보관해요.</p>
</td>
</tr>
</table>

<p align="center"><strong>듣기 → 글로 바꾸기 → 다듬기 → 저장하기</strong></p>

## 🍀 세 걸음이면 완성

| 01 · 준비해요 | 02 · 맡겨요 | 03 · 챙겨요 |
| :--- | :--- | :--- |
| 앱을 켜고 강의 파일을 추가해요. | 모델과 언어를 고르고 **전사 시작**을 눌러요. | 녹취를 확인하고 수정한 뒤 문서나 자막으로 내보내요. |

첫 모델 다운로드는 용량과 저장 위치를 확인하고 동의한 뒤 진행해요. 다운로드가 끝난 모델은 로컬에서 재사용해요.

> **처음이라면** Large-v3 Turbo · 한국어 · FP16으로 시작해보세요.
> 전사가 끝나면 TXT · DOCX · JSON이 자동으로 저장돼요.

<details>
<summary><strong>🧺 실행과 설치 안내 펼치기</strong></summary>

<a href="https://github.com/sungackja/lectureScribe/releases/latest/download/LectureScribe-Setup.exe"><strong>Windows 10/11 x64 설치 파일 다운로드 →</strong></a>

설치 파일을 실행하면 시작 메뉴에 LectureScribe가 추가돼요. 기본 설치 위치는 `%LOCALAPPDATA%\Programs\LectureScribe`이며, 설치 후 앱을 실행해 강의 파일을 등록하면 돼요. 앱과 GPU 라이브러리는 약 2.2GB의 디스크 공간을 사용하고, 전사 모델은 첫 사용 때 별도로 내려받아요.

개발 환경은 Python 3.11 x64에서 `setup.bat`로 설치해요. Qwen은 Python 3.12 또는 uv를 준비하고 `setup_qwen.bat`로 별도 환경을 설치해요.

이 저장소는 프로그램 소개 문서와 설치 파일을 제공해요. 개발 소스와 빌드 방법은 자세한 안내를 참고해주세요.

[설치 · 빌드 · GPU 진단 자세히 보기 →](docs/GUIDE.md#설치와-실행-환경)

</details>

## ⚡ 얼마나 빠를까요?

<p align="center">
  <strong>약 29.8분 강의 한 편</strong><br>
  Large-v3 Turbo의 GPU 전사 시간 <strong>45.7초</strong>
</p>

| 모델 | GPU 전사 시간 | 처리 방식 |
| :--- | ---: | :--- |
| 🌿 Large-v3 Turbo | **45.7초** | FP16 |
| 📚 Large-v3 | 185.7초 | FP16 |
| 🎙️ Qwen3-ASR-1.7B | 394.4초 | BF16 · 60초 청크 |

RTX 5060 Ti에서 측정한 기존 개발 기록이에요. 다운로드 시간은 제외했으며 Qwen은 모델 로딩을 포함하면 총 412.2초예요. 파일과 환경에 따라 결과는 달라져요.

<details>
<summary><strong>🔎 정확도 비교와 검증 범위 읽기</strong></summary>

CLOVA 참고 텍스트와 비교한 CER / WER은 Turbo **6.2% / 14.0%**, Large-v3 **7.2% / 16.9%**, Qwen **5.8% / 15.2%**였어요.

CLOVA 텍스트는 정답지가 아니며, 이 값은 텍스트 간 차이예요. 절대 정확도 점수가 아니고 한국어 띄어쓰기와 화자 표기 차이도 영향을 줘요. 중요한 문장은 원음과 대조해주세요.

[실측 조건과 검증 기록 →](docs/GUIDE.md#실제-측정-결과)

</details>

## 🛠️ 작은 화면 뒤의 구조

<p align="center">
  <strong>PySide6 화면</strong> → <strong>별도 GPU 작업 프로세스</strong> → <strong>문서와 자막</strong>
</p>

화면과 GPU 작업을 나누고, 모델은 작업 프로세스에서 재사용해요. 녹취 원본과 수정본을 따로 보관하고 중지한 작업의 부분 결과도 남겨요.

<details>
<summary><strong>🧩 기술 · 모델 · 저장 위치 자세히 보기</strong></summary>

| 구성 | 사용 기술 |
| :--- | :--- |
| 데스크톱 화면 | PySide6 / Qt |
| Whisper 추론 | faster-whisper / CTranslate2 |
| Qwen 추론 | Qwen-ASR / PyTorch |
| 영상·음성 처리 | PyAV |
| Word 내보내기 | python-docx |
| Windows 배포 | PyInstaller |

모델은 **Turbo · Small · Medium · Large-v3 · Qwen3-ASR-1.7B**를 지원해요. 기본 데이터 저장 위치는 `%LOCALAPPDATA%\LectureScribe`예요.

[모델 안내 →](docs/GUIDE.md#지원-모델) · [제작 구조 →](docs/GUIDE.md#어떻게-만들었나요) · [저장 위치 →](docs/GUIDE.md#저장-위치와-개인정보)

</details>

## 💬 궁금한 것들

<details>
<summary><strong>인터넷 없이 사용할 수 있나요?</strong></summary>

모델 다운로드와 실행 환경 설치에는 인터넷이 필요해요. 준비된 모델로 전사할 때는 내 PC에서 처리해요. 강의 파일을 전사 API에 보내지 않아요.

</details>

<details>
<summary><strong>시간별 노트는 AI 요약인가요?</strong></summary>

발화를 시간 구간으로 묶어 보여주는 기능이에요. 새로운 내용을 생성하거나 요약하지 않아요.

</details>

<details>
<summary><strong>중간에 멈췄다가 이어갈 수 있나요?</strong></summary>

저장된 부분 결과는 보존해요. 재시도는 새 작업으로 처음부터 진행하며, 중단 위치에서 이어하기는 아직 구현되지 않았어요.

</details>

<details>
<summary><strong>사용 전에 알아둘 점이 있나요?</strong></summary>

NVIDIA GPU가 필요하며 CPU 자동 전환은 제공하지 않아요. 다른 PC와 장시간 강의는 추가 검증이 필요해요. 앱 내부 영상 재생과 오디오 트랙 선택은 후속 기능이고, Qwen 시간 표시는 60초 청크 범위예요.

[현재 한계와 후속 기능 →](docs/GUIDE.md#현재-한계와-후속-기능)

</details>

---

<p align="center">
  <strong>오늘의 강의가, 내일의 노트가 되도록 🌷</strong><br>
  <sub>LectureScribe · v0.3.0 · 2026.10.18</sub><br>
  <a href="docs/GUIDE.md">전체 프로그램 안내</a>
</p>

