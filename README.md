# event-market-predictor
import streamlit as st
from textblob import TextBlob

st.set_page_config(page_title="AI Събития и Пазарен Анализ", layout="wide")
st.title("🌍 Въвеждане на глобални събития и прогноза")

# Въвеждане на събитие
st.subheader("📝 Въведи събитие")
event_text = st.text_area("Опиши политическо, икономическо или друго важно събитие")

# Избор на категория
category = st.selectbox("Категория на събитието", ["Геополитика", "Икономика", "Технологии", "Здравеопазване", "Климат", "Друго"])

# Анализ на настроението
if event_text:
    blob = TextBlob(event_text)
    polarity = blob.sentiment.polarity
    if polarity > 0.1:
        sentiment = "Положително"
        forecast = "🟢 Вероятен ръст на пазара"
    elif polarity < -0.1:
        sentiment = "Отрицателно"
        forecast = "🔴 Вероятен спад на пазара"
    else:
        sentiment = "Неутрално"
        forecast = "🟡 Вероятна нестабилност или липса на реакция"

    # Резултат
    st.subheader("🔍 Анализ")
    st.markdown(f"**Настроение:** {sentiment}")
    st.markdown(f"**Категория:** {category}")
    st.markdown(f"**Прогноза:** {forecast}")

    # Вероятност (примерно)
    probability = 80 + int(abs(polarity) * 20)
    st.markdown(f"**Вероятност за вярна прогноза:** {probability}%")
