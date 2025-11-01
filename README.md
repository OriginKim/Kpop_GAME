🎵 노래 맞추기 게임 (Python / Windows)

간단한 콘솔 기반의 노래 제목 맞추기 퀴즈 게임입니다.
.wav 파일을 재생하여 노래 일부를 들려주고, 사용자는 정답을 입력합니다. 기회는 **최대 3번(1초 → 3초 → 5초)**이며, 맞힌 개수로 점수를 집계합니다.

⚠️ Windows 전용
오디오 재생에 winsound 모듈을 사용하므로 Windows 환경에서만 동작합니다. (Python 3.x)

✨ 주요 기능

5문제 랜덤 출제 (중복 없이 셔플)

기회 3번: 1초 → 3초 → 5초 버전 순서로 재생

정답/오답 효과음 지원

대소문자 무시 비교 (.lower() 사용)

게임 종료 후 재시작 선택 가능

🗂️ 파일/폴더 구조 규칙

본 코드는 파일명 규칙에 강하게 의존합니다. 아래 규칙을 반드시 지켜주세요.

project/
├─ game.py                # 본 파이썬 스크립트
├─ correct.wav            # 정답 효과음
├─ wrong.wav              # 오답 효과음
├─ Baddie1.wav            # 1초 버전
├─ Baddie3.wav            # 3초 버전
├─ Baddie5.wav            # 5초 버전
├─ Bubble1.wav
├─ Bubble3.wav
├─ Bubble5.wav
└─ ... (모든 노래 동일 규칙)

🔐 파일명 규칙 (아주 중요)

모든 문제용 노래는 3개의 파일을 가짐: ...1.wav, ...3.wav, ...5.wav

코드가 songs 목록의 파일명에서 끝 5글자(1.wav)를 잘라 3.wav, 5.wav로 치환하여 재생합니다.

예) "Cool With You1.wav" → "Cool With You3.wav", "Cool With You5.wav"

따라서 정확히 1.wav로 끝나도록 이름을 지어야 합니다. (공백 포함 철자 일치)

🧩 정답 매핑 규칙

songs와 answers는 인덱스로 1:1 대응합니다.

songs[i]의 정답은 answers[i]

비교는 .lower()로 수행되며 대소문자 구분 없음

공백/하이픈 등의 차이는 정답 처리에 영향을 줄 수 있으니 answers의 표기를 실제 정답 입력 가이드와 일치시키세요.

예) "Hype boy" vs "Hypeboy" → 현재 코드는 공백 차이를 구분합니다.

🔧 준비물

Python 3.x (Windows)

winsound, time, random (표준 라이브러리)

WAV 파일(PCM 권장)
winsound.PlaySound는 비압축 PCM 형식의 .wav에서 가장 안정적입니다.

▶️ 실행 방법

위의 파일명 규칙을 지킨 .wav 파일들을 스크립트와 같은 폴더에 둡니다.

songs, answers, sound_effect 배열을 실제 파일/정답에 맞게 수정합니다.

터미널(명령 프롬프트)에서 실행:

python game.py


콘솔 안내에 따라 아무 키나 눌러 시작 → 각 문제에서 정답 입력

🧱 배열 설정 가이드
1) 문제용 노래들 (songs)

반드시 1.wav로 끝나는 파일명만 넣습니다.

3초/5초 버전은 자동으로 3.wav, 5.wav로 바꿔 재생합니다.

songs = [
    "Baddie1.wav",
    "Bubble1.wav",
    "Cool With You1.wav",
    # ...
]

2) 정답들 (answers)

songs의 같은 인덱스와 매칭되도록 제목을 적습니다.

대소문자 무시는 하지만 띄어쓰기/특수문자는 구분합니다.

answers = [
    "Baddie",
    "Bubble",
    "Cool With You",
    # ...
]

3) 효과음 (sound_effect)

0번: 정답 / 1번: 오답

sound_effect = [
    "correct.wav",
    "wrong.wav"
]

🕹️ 게임 진행 로직

시작 안내 후, 5문제를 랜덤으로 출제

각 문제:

1차: ...1.wav 재생 → 정답 입력

2차: wrong.wav → ...3.wav 재생 → 재시도

3차: wrong.wav → ...5.wav 재생 → 최종 시도

정답 시 correct.wav 재생 및 점수 +1

3회 모두 오답이면 정답 공개

5문제 종료 후 점수 출력

1 입력 시 다시 시작, 엔터면 종료(ASCII 아트와 함께 종료)

💡 팁 & 주의사항

파일 경로: 현재 코드는 상대경로(실행 폴더 기준)를 사용합니다. 다른 폴더에 두는 경우 절대경로/상대경로를 맞추세요.

포맷 문제: 일부 인코딩된 .wav는 winsound가 못 읽을 수 있습니다. 가급적 PCM(16-bit) .wav로 변환해 사용하세요.

공백/특수문자: 윈도우 파일명에 공백/특수문자가 많으면 오타가 나기 쉽습니다. 가능하면 간결한 이름을 권장합니다.

정답 입력 가독성: 코드에서 .strip()은 없으므로 앞뒤 공백을 넣지 말고 정확히 입력하세요. (개선 아이디어 참고)

🧭 자주 하는 질문(FAQ)

Q. 1초만 재생하는 건가요?
A. 코드가 실제로 재생 시간 제한을 거는 것이 아니라, 1초 길이의 별도 파일(...1.wav)을 재생합니다.
3초/5초도 마찬가지로 미리 잘라둔 파일을 사용합니다.

Q. Windows가 아닌 환경에서는?
A. winsound는 Windows 전용입니다. macOS/Linux에서는 playsound, pydub, simpleaudio 등의 대안을 사용하도록 코드를 바꿔야 합니다.

Q. “Hypeboy”처럼 붙여 쓰거나 띄어쓰기를 다르게 쓰면 오답인가요?
A. 현재 구현에서는 공백/하이픈 차이도 구분합니다. answers 표기를 사용자 안내와 일치시키거나, 비교 로직을 보완하세요. (예: 공백/특수문자 제거 후 비교)

🚀 개선 아이디어 (선택)

입력 전처리 강화:

enter_answer = input(...).strip().lower()
target = answers[song_index].strip().lower()


공백/하이픈 제거 비교:

import re
norm = lambda s: re.sub(r'[\s\-\_&]+', '', s.lower())
if norm(enter_answer) == norm(target):
    ...


파일명 의존도 낮추기: songs에 기본명만 넣고, 재생 시 접미사를 붙이는 방식:

base = "Baddie"
for sec in (1,3,5):
    winsound.PlaySound(f"{base}{sec}.wav", winsound.SND_FILENAME)


오답 시 유사도 힌트(Levenshtein 등) 제공

스코어보드/랭킹, 난이도(출제 수/기회 수) 설정

멀티플레이(번갈아 입력), 카테고리 모드

🧪 요구 사양

OS: Windows 10/11

Python: 3.8+ 권장

오디오: WAV(PCM 16-bit)

콘솔: 기본 CMD/PowerShell 또는 VS Code 터미널

📝 라이선스

개인 학습/취미 용도 자유 사용

상업적 이용 및 배포 시, 음원 저작권을 반드시 확인하고 준수하세요.

🙌 크레딧

코드: 사용자 제공

아이디어/문서화: ChatGPT (README 작성)

테스트 음원/효과음: 각 파일 제공자(사용자)

음원 사용은 저작권법을 준수해주세요.

📣 문의/이슈

파일명이 규칙대로인데도 재생이 안 되면:

경로/파일 철자 확인

WAV 포맷(PCM) 확인

무음 파일로라도 먼저 테스트 (correct.wav, wrong.wav 정상 재생 여부 체크)
