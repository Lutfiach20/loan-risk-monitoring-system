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

## 🔄 Alur Sistem + Visual

### 1️⃣ Workflow BPMN (Camunda)
Proses dimulai dari BPMN yang mengatur alur validasi, perhitungan risk, hingga keputusan.

![BPMN](https://raw.githubusercontent.com/Lutfiach20/loan-risk-monitoring-system/main/workflow.png)

---

### 2️⃣ Worker Memproses Task (Python)
Worker mengambil task dari Camunda (external task) dan menjalankan logic:
- Validate
- Enrich
- Calculate Risk
- Finalize Decision

![Worker](https://raw.githubusercontent.com/Lutfiach20/loan-risk-monitoring-system/main/worker.png)

---

### 3️⃣ Data Masuk ke Elasticsearch & Dilihat di Kibana
Hasil proses (risk & decision) dikirim ke Elasticsearch, lalu bisa diexplore di Kibana.

![Kibana](https://raw.githubusercontent.com/Lutfiach20/loan-risk-monitoring-system/main/kibana.png)

---

### 4️⃣ Monitoring Dashboard di Grafana
Data divisualisasikan dalam bentuk dashboard (pie, bar, dll) untuk monitoring.

![Grafana](https://raw.githubusercontent.com/Lutfiach20/loan-risk-monitoring-system/main/grafana.png)

---

## ⚙️ Logic Business (Python Worker)

### Calculate Risk (berdasarkan amount)

| Range | Risk |
|------|------|
| ≤ 3.000.000 | Low |
| ≤ 10.000.000 | Medium |
| > 10.000.000 | High |

---

### Final Decision

| Risk | Decision |
|------|----------|
| Low | AUTO_APPROVED |
| Medium | MANAGER_APPROVAL |
| High | DIRECTOR_APPROVAL |

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
