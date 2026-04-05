# Rebag Price Tracker

[![Bright Data](https://img.shields.io/badge/Powered%20by-Bright%20Data-blue?style=flat-square)](https://brightdata.de)
[![Rebag Price Tracker](https://img.shields.io/badge/Rebag%20Price%20Tracker-Managed%20Solution-orange?style=flat-square)](https://brightdata.de/products/insights/price-tracker/rebag)
[![Python](https://img.shields.io/badge/Python-3.9%2B-yellow?style=flat-square)](https://python.org)

[![Bright Insights Price Tracker](https://raw.githubusercontent.com/danielshashko/bright-insights-assets/main/price-tracker-hero-v2.png)](https://brightdata.de/products/insights/price-tracker/rebag)

Rebag-Preisverfolgung in Echtzeit – ein US-Marktplatz für authentifizierte gebrauchte Luxus-Handtaschen. Zwei Möglichkeiten für den Einstieg: eine **vollständig verwaltete** Intelligence-Plattform oder ein **benutzerdefinierter Scraper**, erstellt mit dem AI Scraper Builder von Bright Data.

---

## Option 1: Bright Insights - KI-gestützte Preisverfolgung (Empfohlen)

**[Bright Insights](https://brightdata.de/products/insights/price-tracker/rebag)** ist die vollständig verwaltete Retail-Intelligence-Plattform von Bright Data. Keine Scraper zu erstellen, keine Infrastruktur zu warten – nur strukturierte, analysebereite Preisdaten, bereitgestellt für Dashboards, Data Feeds oder Ihre BI-Tools.

**Warum Teams sich für Bright Insights entscheiden:**
- 🚀 **Kein Setup** – In wenigen Minuten live mit sofort einsatzbereiten Dashboards und Data Feeds
- 🤖 **KI-gestützte Empfehlungen** – Ein konversationeller KI-Assistent verwandelt Millionen von Datenpunkten sofort in umsetzbare Erkenntnisse
- ⚡ **Echtzeit-Monitoring** – Stündliche bis tägliche Aktualisierungsraten mit sofortigen Alerts (E-Mail, Slack, webhook)
- 🌍 **Unbegrenzte Skalierung** – Jede Website, jede Geografie, jede Aktualisierungsfrequenz
- 🔗 **Plug-and-play-Integrationen** – AWS, GCP, Databricks, Snowflake und mehr
- 🛡️ **Vollständig verwaltet** – Bright Data übernimmt Schemaänderungen, Website-Updates und Datenqualität automatisch

**Wichtige Anwendungsfälle:**
- ✅ **Überwachen Sie Preise seltener und limitierter Editionen** auf Rebag
- ✅ **Verfolgen Sie die Verfügbarkeit** über Größen und Farben hinweg in Echtzeit
- ✅ **Überprüfen Sie Wiederverkaufsaufschläge** im Vergleich zu Einzelhandelspreisen
- ✅ Überwachen Sie die Einhaltung der MAP-Richtlinie und erkennen Sie Preisverstöße
- ✅ Verfolgen Sie Wettbewerber-Promotions und Promotionsdynamiken
- ✅ Speisen Sie saubere, harmonisierte Daten direkt in dynamische Preisalgorithmen oder KI-Modelle ein

> **Ab $250/Monat – [Erhalten Sie ein individuelles Angebot →](https://brightdata.de/products/insights/price-tracker/rebag)**

---

## Option 2: Erstellen Sie Ihren eigenen Rebag Scraper

Keine vorgefertigte Rebag scraper API? Kein Problem. Der **AI Scraper Builder** von Bright Data generiert in nur wenigen Klicks einen benutzerdefinierten Rebag-Scraper — ganz ohne Programmierung.

### Erstellen Sie Ihren Rebag-Scraper in wenigen Minuten

**[Öffnen Sie den Rebag AI Scraper Builder →](https://brightdata.de/products/web-scraper/rebag)**

Wählen Sie die Domain, beschreiben Sie Ihre Datenanforderungen, und lassen Sie unseren AI Scraper Builder die API automatisch erstellen.

1. **Beschreiben Sie den Datenbedarf in einfachem Englisch**
2. **Die KI generiert sofort die scraper API**
3. **Führen Sie API-Anfragen für sofortige Ergebnisse aus**
4. **Bearbeiten Sie den Code in der integrierten IDE**, falls nötig

Sobald Ihr Scraper erstellt ist, erhält er eine **Web Scraper ID** (`gd_xxxxxxxxxxxx`) — kopieren Sie sie für den Setup-Schritt unten.

### Voraussetzungen

- Python 3.9 oder höher
- Ein [Bright Data account](https://brightdata.de) (kostenlose Testversion verfügbar)
- Ein Bright Data **API token** ([so erhalten Sie einen](https://docs.brightdata.de/general/account/account-settings#api-token))
- Eine **Web Scraper ID** für Rebag (aus dem obigen Build-Schritt)

### Setup

1. **Klonen Sie dieses repository**

   ```bash
   git clone https://github.com/bright-data-de/rebag-price-tracker.git
   cd rebag-price-tracker
   ```

2. **Installieren Sie Abhängigkeiten**

   ```bash
   pip install -r requirements.txt
   ```

3. **Konfigurieren Sie Zugangsdaten**

   Kopieren Sie `.env.example` nach `.env` und tragen Sie Ihre Werte ein:

   ```bash
   cp .env.example .env
   ```

   ```env
   BRIGHTDATA_API_TOKEN=your_api_token_here
   BRIGHTDATA_DATASET_ID=your_dataset_id_here
   ```

   > **Ihre Web Scraper ID**
   > Fügen Sie die Web Scraper ID aus Ihrem [AI Scraper Builder dashboard](https://brightdata.de/products/web-scraper/rebag)
   > in `BRIGHTDATA_DATASET_ID` ein (Format: `gd_xxxxxxxxxxxx`).

---

## Verwendung

Sobald Ihr Rebag-Scraper erstellt wurde und Ihre Web Scraper ID in `.env` konfiguriert ist, funktioniert die Python-Schnittstelle auf die gleiche Weise:

### 1. Bestimmte Produkte per URL verfolgen

Übergeben Sie eine Liste von Rebag-Produkt-URLs, um strukturierte Preisdaten abzurufen:

```python
from price_tracker import track_prices

urls = [
    "https://www.rebag.com/en/products/sample-product-123456",
    # Add more product URLs here
]

results = track_prices(urls)
for item in results:
    print(f"{item.get('title')} - {item.get('final_price', item.get('price'))} {item.get('currency', '')}")
```

Oder direkt ausführen:

```bash
python price_tracker.py
```

### 2. Produkte per Keyword entdecken

Finden Sie Produkte, die einer Keyword-Suche entsprechen:

```python
from price_tracker import discover_by_keyword

results = discover_by_keyword("laptop", limit=50)
```

### 3. Produkte per Kategorie-URL durchsuchen

Sammeln Sie alle Produkte von einer Rebag-Kategorieseite:

```python
from price_tracker import discover_by_category

results = discover_by_category(
    "https://rebag.com/category/example",
    limit=100,
)
```

---

## Ausgabefelder

Jeder Ergebnisdatensatz enthält die folgenden Felder:

| Field | Description |
|-------|-------------|
| `url` | Produktseiten-URL |
| `title` | Produktname |
| `brand` | Marke/Modehaus |
| `price` | Einzelhandelspreis |
| `currency` | Währungscode |
| `in_stock` | Verfügbarkeit |
| `color` | Farbe |
| `size` | Verfügbare Größen |
| `material` | Verwendete Materialien |
| `sku` | SKU / Referenznummer |
| `images` | Produktbilder |
| `description` | Produktbeschreibung |
| `timestamp` | Zeitstempel der Erfassung |

### Beispielausgabe

```json
[
  {
    "url": "https://www.rebag.com/en/products/sample-product-123456",
    "title": "Example Product Name",
    "brand": "Example Brand",
    "initial_price": 59.99,
    "final_price": 44.99,
    "currency": "USD",
    "discount": "25%",
    "in_stock": true,
    "rating": 4.5,
    "reviews_count": 1234,
    "images": ["https://rebag.com/images/product1.jpg"],
    "description": "Product description text...",
    "timestamp": "2025-01-15T10:30:00Z"
  }
]
```

---

## Erweiterte Optionen

Die Funktion `trigger_collection()` akzeptiert optionale Parameter zur Steuerung der Datenerfassung:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | - | Maximale Anzahl zurückzugebender Datensätze |
| `include_errors` | boolean | `true` | Fehlerberichte in die Ergebnisse einschließen |
| `notify` | string (URL) | - | Webhook-URL, die aufgerufen wird, wenn der Snapshot bereit ist |
| `format` | string | `json` | Ausgabeformat: `json`, `csv` oder `ndjson` |

Beispiel mit Optionen:

```python
from price_tracker import trigger_collection, get_results

inputs = [{"url": "https://www.rebag.com/en/products/sample-product-123456"}]
snapshot_id = trigger_collection(inputs, limit=200, notify="https://your-webhook.com/hook")
results = get_results(snapshot_id)
```

---

## Ressourcen

- 🌟 [Rebag Price Tracker - Bright Insights (Managed)](https://brightdata.de/products/insights/price-tracker/rebag)
- 🏗️ [Build a Rebag Scraper](https://brightdata.de/products/web-scraper/rebag)
- 📖 [Bright Data Web Scraper API Documentation](https://docs.brightdata.de/scraping-automation/web-scraper-api/overview)
- 🗄️ [Web Scrapers Control Panel](https://brightdata.de/cp/scrapers)
- 🔑 [How to get an API token](https://docs.brightdata.de/general/account/account-settings#api-token)
- 🌐 [Bright Data Homepage](https://brightdata.de)

---

*Erstellt mit [Bright Data](https://brightdata.de) – der branchenführenden Webdaten-Plattform.*