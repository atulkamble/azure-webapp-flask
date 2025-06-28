 **complete Azure Web App project** example using:

* **Frontend**: HTML + Flask (Python)
* **Backend**: Python Flask API
* **Deployment**: Azure Web App using App Service
* **Infrastructure**: Azure CLI & optional Terraform
* **Extras**: Deployment steps, app settings, and repo structure

---

## 🔧 Project Name: `azure-flask-webapp-demo`

---

## 📁 Project Structure

```
azure-flask-webapp/
├── app/
│   ├── templates/
│   │   └── index.html
│   ├── static/
│   │   └── style.css
│   ├── __init__.py
│   └── app.py
├── requirements.txt
├── runtime.txt
├── startup.txt
├── .azure-pipelines.yml (optional)
├── README.md
└── deploy.sh
```

---

## 🧠 Step-by-Step Code

### `app/app.py`

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")

if __name__ == "__main__":
    app.run(debug=True)
```

---

### `app/templates/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Azure Flask Web App</title>
    <link rel="stylesheet" href="/static/style.css">
</head>
<body>
    <h1>Welcome to Azure Flask Web App!</h1>
    <p>This app is hosted on Azure App Services.</p>
</body>
</html>
```

---

### `app/static/style.css`

```css
body {
    font-family: Arial, sans-serif;
    background-color: #eef;
    padding: 2em;
    text-align: center;
}
```

---

### `requirements.txt`

```
Flask==2.3.3
gunicorn
```

---

### `runtime.txt`

```
python-3.11
```

---

### `startup.txt`

```
gunicorn app.app:app
```

---

## 🚀 Deployment to Azure (Manual)

```bash
# Login to Azure
az login

# Create resource group
az group create --name flask-rg --location eastus

# Create app service plan
az appservice plan create --name flask-plan --resource-group flask-rg --sku FREE

# Create web app
az webapp create --resource-group flask-rg \
  --plan flask-plan \
  --name flask-web-demo-1234 \
  --runtime "PYTHON|3.11" \
  --deployment-local-git

# Set startup command
az webapp config set --resource-group flask-rg --name flask-web-demo-1234 \
  --startup-file startup.txt
```

> Replace `flask-web-demo-1234` with your unique app name.

---

### 🧪 Local Testing

```bash
python app/app.py
```

---

## 🌀 Deployment using Git

```bash
git init
git remote add azure <deploymentGitUrl>  # shown in previous command
git add .
git commit -m "Initial commit"
git push azure master
```

