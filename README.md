🎵 노래 맞추기 게임 (Python / Windows)간단한 콘솔 기반의 노래 제목 맞추기 퀴즈 게임입니다..wav 파일을 재생하여 노래 일부를 들려주고, 사용자는 정답을 입력합니다.기회는 **최대 3번(1초 → 3초 → 5초)**이며, 맞힌 개수로 점수를 집계합니다.⚠️ Windows 전용오디오 재생에 winsound 모듈을 사용하므로 Windows 환경에서만 동작합니다. (Python 3.x)✨ 주요 기능5문제 랜덤 출제 (중복 없이 셔플)기회 3번: 1초 → 3초 → 5초 버전 순서로 재생정답/오답 효과음 지원대소문자 무시 비교 (.lower() 사용)게임 종료 후 재시작 선택 가능🗂️ 파일/폴더 구조본 코드는 파일명 규칙에 강하게 의존합니다. 아래 규칙을 반드시 지켜주세요.project/
├─ game.py        # 본 파이썬 스크립트 (사용자가 실행할 파일)
├─ correct.wav    # 정답 효과음
├─ wrong.wav      # 오답 효과음
├─ Baddie1.wav    # 1초 버전
├─ Baddie3.wav    # 3초 버전
├─ Baddie5.wav    # 5초 버전
├─ Bubble1.wav
├─ Bubble3.wav
├─ Bubble5.wav
└─ ... (모든 노래 동일 규칙)
🔐 파일명 규칙 (중요!)모든 문제용 노래는 3개의 파일을 가짐: ...1.wav, ...3.wav, ...5.wav코드가 songs 목록의 파일명에서 끝 5글자(1.wav)를 잘라 3.wav, 5.wav로 치환하여 재생합니다.예) "Cool With You1.wav" → "Cool With You3.wav", "Cool With You5.wav"따라서 정확히 1.wav로 끝나도록 이름을 지어야 합니다.🧩 정답 매핑 규칙songs와 answers는 인덱스로 1:1 대응합니다.songs[i]: "Cool With You1.wav" → answers[i]: "Cool With You"대소문자 구분은 없지만, 공백 및 특수문자는 비교 시 그대로 사용됩니다.예: "Hype boy"와 "Hypeboy"는 서로 다른 답으로 처리됩니다.🔧 준비물 및 환경Python 3.x (Windows)winsound, time, random (표준 라이브러리)WAV 파일(PCM 권장) — winsound.PlaySound는 비압축 PCM .wav에서 가장 안정적▶️ 실행 방법위의 파일명 규칙을 지킨 .wav 파일들을 game.py와 같은 폴더에 둡니다.songs, answers, sound_effect 배열을 실제 파일/정답에 맞게 수정합니다.터미널(명령 프롬프트/PowerShell)에서 실행:python game.py
