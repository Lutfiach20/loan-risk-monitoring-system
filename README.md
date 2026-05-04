# Loan Risk Monitoring System

Sistem workflow pemrosesan pengajuan pinjaman menggunakan **Camunda BPMN**, diproses oleh **Python Worker**, dan dimonitor menggunakan **Elasticsearch, Kibana, dan Grafana**.

---

## 🧠 Arsitektur

Camunda → Worker (Python) → Elasticsearch → Kibana / Grafana

---

## 🔄 Alur Sistem

### 1. Workflow (Camunda)
BPMN mengatur seluruh alur proses pinjaman dari awal sampai akhir.

![BPMN](https://raw.githubusercontent.com/Lutfiach20/loan-risk-monitoring-system/main/workflow.png)

---

### 2. Processing (Python Worker)
Worker mengambil task dari Camunda dan menjalankan logic:
- Validasi data
- Perhitungan risk
- Penentuan decision

![Worker](https://raw.githubusercontent.com/Lutfiach20/loan-risk-monitoring-system/main/worker.png)

---

### 3. Data Monitoring (Kibana)
Data hasil proses dikirim ke Elasticsearch dan bisa dianalisa di Kibana.

![Kibana](https://raw.githubusercontent.com/Lutfiach20/loan-risk-monitoring-system/main/kibana.png)

---

### 4. Dashboard (Grafana)
Visualisasi data dalam bentuk dashboard monitoring.

![Grafana](https://raw.githubusercontent.com/Lutfiach20/loan-risk-monitoring-system/main/grafana.png)

---

## ⚙️ Logic

**Risk Level**
- Low: ≤ 3 juta  
- Medium: ≤ 10 juta  
- High: > 10 juta  

**Decision**
- Low → Auto Approved  
- Medium → Manager Approval  
- High → Director Approval  

---

## 🚀 Run

```bash
pip install requests
python worker.py
