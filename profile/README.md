# 🛡️ Project Pentagon

**Project Pentagon** adalah arsitektur infrastruktur modern berbasis container yang dirancang untuk mendukung aplikasi Laravel dalam skala multi-service dan multi-tenant, dengan fokus pada **scalability**, **maintainability**, dan **production readiness**.

---

## 🧠 Architecture Overview

Berikut adalah gambaran alur sistem:

<svg width="900" height="600" viewBox="0 0 900 600" xmlns="http://www.w3.org/2000/svg">
  <style>
    .box { fill: #0f172a; stroke: #38bdf8; stroke-width: 2; rx: 10; }
    .text { fill: #e2e8f0; font-family: Arial, sans-serif; font-size: 14px; text-anchor: middle; }
    .title { font-size: 16px; font-weight: bold; }
    .arrow { stroke: #94a3b8; stroke-width: 2; marker-end: url(#arrowhead); }
  </style>

  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="7" 
    refX="10" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#94a3b8"/>
    </marker>
  </defs>

  <!-- Client -->
  <rect x="350" y="20" width="200" height="50" class="box"/>
  <text x="450" y="50" class="text title">Client</text>

  <!-- Cloudflare -->
  <rect x="350" y="100" width="200" height="50" class="box"/>
  <text x="450" y="130" class="text title">Cloudflare</text>

  <!-- Traefik -->
  <rect x="350" y="180" width="200" height="50" class="box"/>
  <text x="450" y="210" class="text title">Traefik</text>
  <text x="450" y="225" class="text">(Reverse Proxy + SSL)</text>

  <!-- Docker Network Container -->
  <rect x="150" y="260" width="600" height="300" fill="none" stroke="#38bdf8" stroke-width="2" rx="15"/>
  <text x="450" y="280" class="text title">Docker Network</text>

  <!-- Services -->
  <rect x="200" y="300" width="200" height="50" class="box"/>
  <text x="300" y="330" class="text">Laravel App</text>

  <rect x="500" y="300" width="200" height="50" class="box"/>
  <text x="600" y="330" class="text">Queue Worker</text>

  <rect x="200" y="380" width="200" height="50" class="box"/>
  <text x="300" y="410" class="text">Scheduler</text>

  <rect x="500" y="380" width="200" height="50" class="box"/>
  <text x="600" y="410" class="text">Redis</text>

  <rect x="200" y="460" width="200" height="50" class="box"/>
  <text x="300" y="490" class="text">MinIO</text>

  <rect x="500" y="460" width="200" height="50" class="box"/>
  <text x="600" y="490" class="text">Database</text>

  <!-- Arrows -->
  <line x1="450" y1="70" x2="450" y2="100" class="arrow"/>
  <line x1="450" y1="150" x2="450" y2="180" class="arrow"/>
  <line x1="450" y1="230" x2="450" y2="260" class="arrow"/>

</svg>


---

## 🚀 Core Components

### 🌐 Cloudflare
- DNS Management
- CDN & Caching
- SSL/TLS termination (optional)
- DDoS Protection

---

### 🔀 Traefik (Reverse Proxy)
- Dynamic routing berbasis container
- Automatic SSL (Let's Encrypt / Cloudflare)
- Middleware support (rate limit, auth, dll)

---

### 🐳 Docker Environment
Semua service berjalan dalam isolated container untuk konsistensi environment dan kemudahan deployment.

---

### ⚙️ Laravel Application
- Mendukung arsitektur:
  - Multi-service (modular)
  - Multi-tenant (shared / isolated)
- Terpisah antara:
  - App container
  - Queue worker
  - Scheduler

---

### 📦 Queue Worker
- Menjalankan job asynchronous
- Menggunakan Redis sebagai backend

---

### ⏱️ Scheduler
- Menjalankan cron job Laravel (`schedule:run`)
- Dipisah dari container utama untuk reliability

---

### 🗄️ Database
- Menggunakan:
  - MySQL (recommended)
  - MariaDB (optional)
- Engine:
  - InnoDB (default & production ready)

---

### 🪣 MinIO (Object Storage)
- S3-compatible storage
- Digunakan untuk:
  - File upload
  - Asset storage
  - Backup

---

### ⚡ Redis
- Cache layer
- Queue driver
- Session storage
- Performance booster untuk aplikasi

---

## 🧱 Design Principles

- **Separation of Concerns**  
  Setiap service berjalan dalam container terpisah

- **Scalability First**  
  Mudah scale horizontal (app, worker, dll)

- **Production Ready**  
  Dirancang untuk kebutuhan real-world & enterprise

- **Cloud Agnostic**  
  Bisa dijalankan di VPS, cloud, maupun hybrid

---

## ⚠️ Best Practices

- Gunakan volume untuk persistence (DB & storage)
- Pisahkan container:
  - App
  - Worker
  - Scheduler
- Aktifkan logging sejak awal
- Gunakan Redis untuk performa optimal
- Siapkan strategi backup (DB & MinIO)

---

## 📌 Roadmap (Optional)

- [ ] Database replication (master-slave)
- [ ] Horizontal scaling (multi-node)
- [ ] Observability (Prometheus, Grafana)
- [ ] Centralized logging (ELK / Loki)
- [ ] Kubernetes migration (future)

---

## 🤝 Contributing

Kontribusi terbuka untuk pengembangan arsitektur dan improvement sistem.  
Silakan buat issue atau pull request.

---

## 📄 License

MIT License
