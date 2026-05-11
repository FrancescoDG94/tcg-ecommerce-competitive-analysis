<div align="center">
  <img src="Logo.png" alt="A&I Trading" width="200"/>
  
  # TCG E-commerce — Analisi Competitiva del Mercato Trading Card Games
  
  **Capstone Project · Master in Data Analytics & AI · Epicode**
  
  ![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat&logo=python&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat&logo=mysql&logoColor=white)
  ![Power BI](https://img.shields.io/badge/Power_BI-Desktop-F2C811?style=flat&logo=powerbi&logoColor=black)
  ![DAX](https://img.shields.io/badge/DAX-Measures-1E40AF?style=flat)
  ![Status](https://img.shields.io/badge/Status-Completed-success?style=flat)
  
</div>

---

## 🎯 Il problema di business

A&I Trading è un retailer specializzato nella distribuzione di Trading Card Games (Magic: The Gathering, Pokémon, One Piece) che opera nei mercati USA ed EU.

**Domanda di business:**

> Come ci posizioniamo rispetto ai principali competitor in termini di prezzo, profondità di catalogo e disponibilità di prodotti?

Per rispondere, è stata costruita una **pipeline end-to-end** che raccoglie dati di prezzo e disponibilità da 3 e-commerce competitor reali, li struttura in un database relazionale, e li trasforma in insight azionabili tramite una dashboard interattiva Power BI con AI integrata.

---

## 📊 Insight principali

| Metrica | Valore | Implicazione |
|---|---|---|
| **Prodotti scrapati** | 884 | Da 3 e-commerce reali |
| **Prodotti unici** (post-deduplicazione) | 254 | Granularità di analisi |
| **Prodotti confrontabili** (su 2+ competitor) | 105 | Set per analisi competitiva diretta |
| **CoolStuffInc è più economico nel** | **49%** dei casi | Leader di pricing |
| **Out-of-stock CoolStuffInc su Magic/Pokémon** | **78,75%** | Catalogo vetrina, non operativo |
| **Risparmio medio per prodotto** | **$42 USD** | Opportunità di pricing per A&I |
| **Picco di risparmio (Final Fantasy Collector Box)** | **$920 USD** | Top outlier identificato |

---

## 🏗 Architettura tecnica

```
┌─────────────────┐     ┌──────────────┐     ┌─────────────────┐     ┌──────────────┐
│   3 SCRAPER     │     │     ETL      │     │     MYSQL       │     │   POWER BI   │
│   (Python +     │ ──▶ │   PANDAS +   │ ──▶ │  Modello stella │ ──▶ │  Dashboard   │
│   Selenium +    │     │   CANONIC.   │     │   7 tabelle     │     │   6 pagine   │
│   BeautifulSoup)│     │              │     │   7 viste SQL   │     │   AI nativa  │
└─────────────────┘     └──────────────┘     └─────────────────┘     └──────────────┘
       │                       │                      │                      │
       ▼                       ▼                      ▼                      ▼
   884 prodotti           254 canonici          Schema relazionale     Insight azionabili
```

### Stack tecnologico

- **Python 3.11** — Web scraping (Selenium, BeautifulSoup, Requests), data manipulation (pandas)
- **MySQL 8.0** — Database relazionale con modello a stella + 7 viste analitiche SQL
- **Power BI Desktop** — Dashboard con misure DAX dinamiche, formattazione condizionale, AI integrata (Decomposition Tree)
- **AI Agent** — Pulsante con WebUrl dinamica che lancia ricerche Google contestuali

---

## 📂 Struttura del repository

```
Capstone Project/
│
├── README.md                                  Questo file
├── Logo.png                                   Brand identity A&I Trading
│
├── Miniaturemarket Scraper Finale.ipynb       Web scraping competitor USA #1
├── Coolstuffinc Scraper Finale.ipynb          Web scraping competitor USA #2
├── Il Covo del Nerd Scraper Finale.ipynb      Web scraping competitor EU/Italia
│
├── MiniatureMarket export/
│   └── miniaturemarket_raw.csv                Dataset grezzo competitor USA #1
├── CoolStuffInc export/
│   └── csi_raw.csv                            Dataset grezzo competitor USA #2
├── Il Covo del Nerd export/
│   └── icn_raw.csv                            Dataset grezzo competitor EU
│
├── Estrapolazione prodotti.ipynb              ETL: pulizia e canonicalizzazione
├── Creazione Dataset su Mysql.ipynb           Setup schema MySQL via Python
├── Import dati su My SQL.ipynb                Caricamento dati nel database
├── Viste Analitiche.ipynb                     Generazione 7 viste SQL
├── Database SQL.sql                           DDL + DML + viste (standalone)
│
├── Output per my sql/
│   └── viste_analitiche/                      Export CSV delle 7 viste analitiche
│       ├── v_pricing_canonico.csv
│       ├── v_pricing_canonico_confrontabili.csv
│       ├── v_gap_competitivo.csv
│       ├── v_catalog_depth.csv
│       ├── v_price_tier.csv
│       ├── v_market_overview.csv
│       └── v_savings_opportunity.csv
│
└── TCG Competitive Analysis.pbix              Dashboard Power BI finale
```

---

## 🚀 Come riprodurre il progetto

### Prerequisiti

- Python 3.11+
- MySQL 8.0+ con MySQL Workbench
- Power BI Desktop (Windows)
- Chrome installato (per Selenium)

### Setup

1. **Clona il repository**
   ```bash
   git clone https://github.com/FrancescoDG94/tcg-ecommerce-competitive-analysis.git
   cd tcg-ecommerce-competitive-analysis
   ```

2. **Installa le dipendenze Python**
   ```bash
   pip install selenium beautifulsoup4 lxml pandas tqdm mysql-connector-python sqlalchemy requests
   ```

3. **Crea il database MySQL**
   - Apri MySQL Workbench
   - File → Open SQL Script → seleziona `Database SQL.sql`
   - Esegui (Ctrl+Shift+Enter) — crea database, tabelle e 7 viste analitiche

4. **Esegui lo scraping** (opzionale, i CSV sono già forniti nelle cartelle `*export/`)
   - Apri i 3 notebook scraper in ordine
   - Esegui — ogni notebook produce un CSV nella relativa cartella `export/`

5. **Esegui ETL e import in MySQL**
   - Apri `Estrapolazione prodotti.ipynb` ed eseguilo (canonicalizzazione)
   - Apri `Import dati su My SQL.ipynb`, inserisci le tue credenziali MySQL, ed eseguilo
   - Apri `Viste Analitiche.ipynb` ed eseguilo per generare le 7 viste

6. **Apri la dashboard**
   - Apri `TCG Competitive Analysis.pbix` in Power BI Desktop
   - Configura la connessione MySQL con le tue credenziali
   - Refresh dei dati

---

## 🎓 Decisioni di design notevoli

### 1. Canonicalizzazione dei prodotti
Stesso prodotto venduto da competitor diversi viene riconosciuto come **stessa entità canonica** tramite pipeline di matching su set, tipologia, lingua e variante. Riduce 884 listing a 254 prodotti unici, di cui 105 confrontabili (presenti su 2+ competitor).

### 2. Normalizzazione tax-excluded
Il Covo del Nerd vende con IVA italiana (22%) inclusa, mentre i retailer USA non includono sales tax (applicata al checkout). I prezzi vengono normalizzati tax-excluded per garantire **confronti omogenei**:
```sql
-- Prezzo ICN normalizzato a USD tax-excluded
ROUND(po.price / 1.22 * 1.13, 2) AS price_icn_usd_net
```

### 3. Tasso di cambio EUR→USD fissato
Snapshot a data fissa (4 maggio 2026, tasso ECB indicativo = 1.13). Costante documentata in vista SQL per ricalcolo facile su nuovi snapshot.

### 4. Integrazione AI
Dashboard con due livelli di AI:
- **Decomposition Tree nativo Power BI** → esplorazione dinamica dei prezzi per dimensione
- **AI Agent custom** → pulsante con misura DAX che genera URL Google contestuale per il prodotto selezionato

---

## 🎬 Demo video

[![Video presentazione](https://img.shields.io/badge/▶_Guarda_su_LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/francesco-della-gatta/)

> Video di presentazione di 2:30 minuti che illustra l'intera pipeline e gli insight di business.

---

## 👤 Autore

<table>
  <tr>
    <td>
      <strong>Francesco Della Gatta</strong><br>
      Data Analyst · Capstone Project Epicode (Maggio 2026)<br><br>
      <a href="www.linkedin.com/in/francescodellagatta">
        <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white" alt="LinkedIn"/>
      </a>
      <a href="https://github.com/FrancescoDG94">
        <img src="https://img.shields.io/badge/GitHub-181717?style=flat&logo=github&logoColor=white" alt="GitHub"/>
      </a>
    </td>
  </tr>
</table>

---

## 📜 Licenza

Questo progetto è un capstone accademico ed è condiviso a scopo dimostrativo del percorso formativo. I dati scrapati sono utilizzati solo per analisi statistica aggregata e non sono ridistribuiti.

---

<div align="center">
  <sub>Costruito con ❤️ a Roma — Maggio 2026</sub>
</div>
