# atlas-v1
import streamlit as st
import yfinance as yf

st.title("🏦 Atlas v7 Working Version")

def get_market():
    return {
        "gold": yf.Ticker("GC=F").history(period="1d")["Close"].iloc[-1],
        "dxy": yf.Ticker("DX-Y.NYB").history(period="1d")["Close"].iloc[-1],
        "vix": yf.Ticker("^VIX").history(period="1d")["Close"].iloc[-1],
    }

m = get_market()

st.subheader("Market Data")
st.json(m)

score = 0
if m["dxy"] > 105:
    score -= 1
if m["vix"] > 20:
    score += 1

st.subheader("Signal")

if score > 0:
    st.write("BUY GOLD")
elif score < 0:
    st.write("SELL GOLD")
else:
    st.write("NO TRADE")