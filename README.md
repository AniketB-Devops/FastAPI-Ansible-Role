# 🚀 Ansible Role: FastAPI Deployment

![Ansible](https://img.shields.io/badge/Ansible-2.9+-red)
![Platform](https://img.shields.io/badge/Platform-Ubuntu-blue)
![Python](https://img.shields.io/badge/Python-3.x-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## 📌 Project Overview

`advance-handlers` is an Ansible role that installs and configures a **FastAPI** application with systemd service management.

This role is designed to demonstrate **advanced Ansible handler concepts**, including:

- ✅ Standard Handlers  
- ✅ Conditional Handlers  
- ✅ Immediate Handler Execution (`meta: flush_handlers`)  
- ✅ Loop-triggered Handlers  
- ✅ Service Restart & Reload Logic  

It is ideal for DevOps learning, handler behavior demonstration, and systemd automation practice.

---

## 🏗 Architecture Overview

```
Ansible Role
     │
     ├── Install Python & Pip
     ├── Install FastAPI & Uvicorn
     ├── Create Application Directory
     ├── Deploy FastAPI App
     ├── Deploy systemd Service
     └── Manage Service via Handlers
```

FastAPI runs via:

```
uvicorn main:app --host 0.0.0.0 --port 8000
```

Managed by:

```
systemd → fastapi-demo.service
```

---

## 📦 Role Variables

Defined in `defaults/main.yml`

| Variable | Description | Default |
|----------|------------|---------|
| fastapi_dir | Directory for application files | `/opt/fastapi_app` |
| fastapi_service | systemd service name | `fastapi-demo.service` |
| python_pkg | Python package variant | `uvicorn[standard]` |

---

## 📁 Role Structure

```
advance-handlers/
├── defaults/
│   └── main.yml
├── handlers/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
│   └── fastapi.service.j2
└── README.md
```

---

## ⚙️ What This Role Does

### 1️⃣ Installs Dependencies
- Python3
- pip
- FastAPI
- Uvicorn

### 2️⃣ Creates Application Directory
```
/opt/fastapi_app
```

### 3️⃣ Deploys FastAPI App

Sample endpoint:

```python
@app.get("/")
def read_root():
    return {"Hello": "World"}
```

### 4️⃣ Deploys systemd Unit

```
/etc/systemd/system/fastapi-demo.service
```

### 5️⃣ Demonstrates Advanced Handlers

| Handler Type | Purpose |
|--------------|----------|
| Restart Handler | Restarts FastAPI service |
| Reload Handler | Reloads service |
| Conditional Handler | Runs only on Ubuntu |
| Loop Handler | Triggered by loop tasks |
| Immediate Handler | Forced execution mid-play |

---

## 🛠 Example Playbook

```yaml
---
- hosts: localhost
  become: yes
  roles:
    - advance-handlers
```

---

## ▶️ Run the Role

```bash
ansible-playbook -i inventory playbook.yml
```

---

## 🔄 Handler Demonstration Flow

The role intentionally includes:

- `notify`
- `meta: flush_handlers`
- OS-based conditional execution
- Loop-based notifications

This makes it a strong example for advanced handler learning.

---

## 🧪 Verification

Check service status:

```bash
systemctl status fastapi-demo.service
```

Test endpoint:

```
http://localhost:8000
```

Expected output:

```json
{"Hello": "World"}
```

---

## 📚 Learning Outcomes

This project demonstrates:

- Real-world handler management
- Idempotency principles
- Service automation
- Systemd integration with Ansible
- Role structuring best practices

---

## 👨‍💻 Author

**Aniket Barhate**  
Middleware Application Support & DevOps Engineer  
5+ Years Experience  

---
