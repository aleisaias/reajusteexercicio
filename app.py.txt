import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

# ============================
# Base de dados
# ============================
data = {
    "Reajuste 2026": [
        14.5, 14.0, 13.0, 12.0, 11.5, 11.3, 11.2, 11.1, 11.0,
        10.7, 10.0, 9.5, 9.0, 8.0
    ],
    "Alunos": [
        5318, 86, 5672, 11514, 18025, 599, 4174, 9685, 82304,
        3524, 30620, 1158, 2651, 11857
    ],
    "Percentual": [
        2.84, 0.05, 3.03, 6.15, 9.63, 0.32, 2.23, 5.17, 43.97,
        1.88, 16.36, 0.62, 1.42, 6.33
    ]
}

df = pd.DataFrame(data)

# Ordenar reajustes em ordem crescente
df = df.sort_values("Reajuste 2026")

# ============================
# Gráfico
# ============================
st.title("Distribuição de Alunos por Faixa de Reajuste 2026")

fig, ax = plt.subplots(figsize=(12,6))

bars = ax.bar(df["Reajuste 2026"].astype(str) + "%", df["Percentual"], color="#4C72B0")

# Rótulos no topo (horizontal)
for bar, pct in zip(bars, df["Percentual"]):
    ax.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.3,
             f"{pct:.2f}%", ha="center", va="bottom", fontsize=9, rotation=0)

ax.set_xlabel("Faixa de Reajuste (%)", fontsize=12)
ax.set_ylabel("Percentual de Alunos (%)", fontsize=12)

# Exibe o gráfico no Streamlit
st.pyplot(fig)
