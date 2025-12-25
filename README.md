# 전고점/전저점 시장 분석

부동산 시장의 전고점(이전 최고가) 및 전저점(이전 최저가) 대비 회복률을 분석하고 시각화하는 데이터 분석 프로젝트입니다.

## 주요 기능

- 📊 **읍면동 단위 상세 분석**: 지역별 전고점/전저점 대비 회복률 분석
- 📈 **시각화**: 파이 차트를 활용한 직관적인 데이터 시각화
- 🎨 **색상 구분**: 회복률 구간별 색상으로 한눈에 파악
  - 🔴 빨간색 계열: 상승 (0~10%, 10~20%, 20~30%, 30% 이상)
  - 🔵 파란색 계열: 하락 (0~-10%, -10~-20%, -20~-30%, -30% 이상)
  - ⚫ 회색: 거래 없음
- 🖋️ **한글 폰트 자동 설정**: 운영체제별 최적의 한글 폰트 자동 선택

## 기술 스택

- **Python**: 3.11+
- **패키지 관리**: [uv](https://docs.astral.sh/uv/) (빠른 Python 패키지 관리 도구)
- **데이터 분석**: pandas, matplotlib
- **파일 처리**: openpyxl
- **개발 환경**: Jupyter Notebook

## 빠른 시작

### 1. uv 설치

```bash
# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Homebrew (macOS)
brew install uv

# 설치 확인
uv --version
```

### 2. 의존성 설치

```bash
# 프로젝트 디렉토리로 이동
cd /Users/foodie/myproject/전고점

# 모든 의존성 자동 설치
uv sync
```

### 3. Jupyter Notebook 실행

```bash
# Jupyter Notebook 실행
uv run jupyter notebook

# 또는 Jupyter Lab 실행
uv run jupyter lab
```

### 4. 분석 시작

1. Jupyter에서 `dong_check.ipynb` 또는 `sigungu_check.ipynb` 파일 열기
2. 데이터 파일 준비: `~/Downloads/전고점 진단_읍면동.xlsx` 또는 `~/Downloads/전저점 진단_읍면동.xlsx`
3. 셀을 순서대로 실행

## 프로젝트 구조

```
전고점/
├── .venv/                     # uv가 생성한 가상환경
├── dong_check.ipynb           # 읍면동 단위 전고점 분석
├── sigungu_check.ipynb        # 시군구 단위 분석
├── dong_analysis_overall.png  # 분석 결과 예시
├── pyproject.toml             # 프로젝트 설정 및 의존성
├── .python-version            # Python 버전 (3.11)
├── main.py                    # 메인 스크립트
└── README.md                  # 이 파일
```

## uv 사용 가이드

### 기본 명령어

```bash
# 패키지 추가
uv add <패키지명>

# 패키지 제거
uv remove <패키지명>

# Python 스크립트 실행
uv run python <스크립트명>.py

# 설치된 패키지 목록
uv pip list

# 의존성 업데이트
uv sync --upgrade
```

### uv vs pip/venv 비교

| 작업 | 기존 방식 | uv |
|------|---------|-----|
| 가상환경 생성 | `python -m venv venv` | `uv init` |
| 가상환경 활성화 | `source venv/bin/activate` | 불필요 (`uv run` 사용) |
| 패키지 설치 | `pip install pandas` | `uv add pandas` |
| 스크립트 실행 | `python script.py` | `uv run python script.py` |
| Jupyter 실행 | `jupyter notebook` | `uv run jupyter notebook` |

### uv의 장점

✅ **속도**: Rust로 작성되어 pip보다 10-100배 빠름
✅ **간편함**: 가상환경 + 패키지 관리를 하나의 도구로
✅ **정확성**: 더 나은 의존성 해결
✅ **디스크 효율**: 글로벌 캐시로 공간 절약

## 데이터 형식

### 필요한 Excel 파일

- **파일명**: `전고점 진단_읍면동.xlsx` 또는 `전저점 진단_읍면동.xlsx`
- **위치**: `~/Downloads/` 폴더
- **구조**:

| 시도 | 시군구 | 읍면동 | 회복률 구간 | 비율 |
|------|--------|--------|------------|------|
| 서울 | 강남구 | 역삼동 | 30% 이상 상승 | 15.5 |
| 서울 | 강남구 | 역삼동 | 20~30% 상승 | 25.3 |
| ... | ... | ... | ... | ... |

## 사용 예시

### 노트북에서 분석 실행

```python
# 한글 폰트 설정
setup_korean_font()

# 데이터 로드 및 처리
all_districts_data = load_and_process_excel_data()

# 특정 구의 데이터 시각화
if all_districts_data:
    for district_name, dong_data in all_districts_data.items():
        print(f"--- {district_name} 차트 생성 ---")
        visualize_single_district(district_name, dong_data)
```

## 문제 해결

### Jupyter 커널이 보이지 않을 때

```bash
# 커널 수동 설치
uv run python -m ipykernel install --user --name=market-analysis

# Jupyter 재시작
uv run jupyter notebook
```

### 가상환경 재생성

```bash
# .venv 폴더 삭제
rm -rf .venv

# 의존성 재설치
uv sync
```

### 한글 폰트 오류

노트북에서 `setup_korean_font()` 함수가 운영체제별 폰트를 자동으로 설정합니다:
- **macOS**: AppleGothic 또는 D2Coding
- **Windows**: Malgun Gothic
- **Linux**: NanumGothic

## 개발 환경

- Python 3.11.12
- macOS (Darwin 24.6.0)
- uv 0.7.18

## 라이선스

개인 학습 및 분석 목적의 프로젝트입니다.

## 참고 자료

- [uv 공식 문서](https://docs.astral.sh/uv/)
- [Pandas 문서](https://pandas.pydata.org/docs/)
- [Matplotlib 갤러리](https://matplotlib.org/stable/gallery/index.html)
- [Jupyter Notebook 문서](https://jupyter-notebook.readthedocs.io/)

---

**Vibe Coding으로 즐겁게 개발하세요!** 🎉
