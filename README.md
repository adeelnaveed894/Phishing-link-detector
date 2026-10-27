# Phishing-link-detector
Python code to detect suspicious link

import streamlit as st
from urllib.parse import urlparse

st.title("🔐 Suspicious Link Checker")
st.write("Check a URL for common warning signs.")

def check_link(url):
    parsed = urlparse(url)
    warnings = []

    if parsed.scheme != "https":
        warnings.append("No HTTPS security")

    if parsed.username or parsed.password:
        warnings.append("Suspicious login information")

    if "xn--" in parsed.netloc:
        warnings.append("Potentially misleading domain")

    if len(url) > 150:
        warnings.append("Unusually long URL")

    return warnings

url = st.text_input("Enter a URL")

if st.button("Check Link"):
    if not url:
        st.warning("Please enter a URL.")
    else:
        warnings = check_link(url)

        if warnings:
            st.error("Potential warning signs found:")
            for warning in warnings:
                st.write("⚠️", warning)
        else:
            st.success("No obvious warning signs found.")
