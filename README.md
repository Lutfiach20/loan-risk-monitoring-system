# Loan Risk Monitoring System (Camunda + Python + Elasticsearch + Grafana)

Project ini merupakan implementasi sistem workflow pemrosesan pengajuan pinjaman menggunakan **Camunda BPMN** yang terintegrasi dengan **Python Worker**, serta monitoring menggunakan **Elasticsearch, Kibana, dan Grafana**.

---

## 🔧 Teknologi yang Digunakan
- Camunda BPMN (Workflow Engine)
- Python (External Task Worker)
- Elasticsearch (Data Storage)
- Kibana (Data Exploration)
- Grafana (Dashboard Monitoring)

---

## 🧠 Arsitektur Sistem

Camunda → Python Worker → Elasticsearch → Kibana / Grafana

---

## 🔄 Alur Sistem

1. User menginput data pengajuan pinjaman
2. Camunda menjalankan workflow BPMN
3. Python worker mengambil task (external task)
4. Worker memproses:
   - Validate data
   - Enrich data
   - Hitung risk
   - Tentukan decision
5. Data dikirim ke Elasticsearch
6. Data divisualisasikan di Kibana & Grafana

---

## ⚙️ Python Worker

Worker bertugas mengambil task dari Camunda dan memproses logic bisnis.

### Proses yang dilakukan:

### 1. Validate Data
- Mengecek apakah data valid
- Output: `isValid = true/false`

---

### 2. Enrich Data
- Simulasi enrichment data (dummy process)

---

### 3. Calculate Risk
Berdasarkan jumlah pinjaman (`amount`):

| Range | Risk |
|------|------|
| ≤ 3.000.000 | Low |
| ≤ 10.000.000 | Medium |
| > 10.000.000 | High |

---

### 4. Finalize Decision

| Risk | Decision |
|------|----------|
| Low | AUTO_APPROVED |
| Medium | MANAGER_APPROVAL |
| High | DIRECTOR_APPROVAL |

---

### 5. Send to Elasticsearch
Data dikirim untuk kebutuhan monitoring dan visualisasi

---

## 📊 Contoh Data Output (Elasticsearch)

```json
{
  "networkOrder": "N0101",
  "riskLevel": "low",
  "decision": "AUTO_APPROVED",
  "amount": 1000000,
  "income": 12000000,
  "creditScore": 780,
  "age": 25,
  "tenure": 6,
  "existingLoan": 0,
  "timestamp": "2026-05-04T10:00:00Z"
}
