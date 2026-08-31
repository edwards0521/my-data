import streamlit as st
import pandas as pd

# 페이지 설정
st.set_page_config(
    page_title="서울 100년 기온 변화",
    page_icon="🌡️",
    layout="wide"
)

st.title("🌡️ 서울의 100년 기온 변화")
st.write("서울의 일별 기온 데이터를 이용해 연평균 기온의 변화를 살펴봅니다.")

# 데이터 주소
DATA_URL = "https://raw.githubusercontent.com/greatsong/modudata/main/data/seoul.csv"

# 데이터 읽기
df = pd.read_csv(DATA_URL)

# 날짜 열을 날짜 형식으로 변환
df["날짜"] = pd.to_datetime(df["날짜"])

# 연도 추출
df["연도"] = df["날짜"].dt.year

# 연도별 평균기온 계산
annual_temp = (
    df.groupby("연도")["평균기온"]
    .mean()
    .reset_index()
)

# 요약통계
st.subheader("📊 요약통계")
st.dataframe(
    df[["평균기온", "최저기온", "최고기온"]].describe()
)

# 연평균 기온 그래프
st.subheader("📈 서울 연평균 기온의 변화")

st.line_chart(
    annual_temp.set_index("연도")["평균기온"]
)

st.caption(
    "※ 그래프의 한 해 값은 해당 연도의 일별 평균기온을 평균한 연평균 기온입니다."
