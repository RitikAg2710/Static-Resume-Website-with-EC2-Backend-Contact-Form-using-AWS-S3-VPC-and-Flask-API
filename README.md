# Static-Resume-Website-with-EC2-Backend-Contact-Form-using-AWS-S3-VPC-and-Flask-API

# 💼 Static Resume Website with EC2-Backend Contact Form using AWS S3, VPC, and Flask API

This project showcases a production-ready DevOps setup where a static resume website is hosted on **Amazon S3**, and the contact form submits data to a **Flask API** hosted on an **EC2 instance** within a **manually created VPC**.

---

## 🧠 Features

- 📄 Resume hosted as a static website using **AWS S3**
- 🧾 Contact form sends data to a **Flask backend**
- 🌐 Flask runs on **EC2 inside a custom VPC**
- 🔁 Full **VPC routing + public subnet + internet gateway**
- 🔐 CORS enabled, custom **Security Group** on port `5000`
- ☁️ Optional: Connect through **CloudFront** and/or API Gateway

---

## 🔧 Technologies Used

- AWS S3 (static website hosting)
- AWS EC2 (Flask backend)
- AWS VPC (manual setup with subnet + routing)
- Flask (Python web framework)
- HTML/CSS + Fetch API
- Linux (Ubuntu, bash)
- Security Groups, Ingress Rules
- Flask-CORS

---

## 🚀 How It Works

1. `index.html` is hosted on S3 with resume and a contact form
2. On form submit, a `POST` request is made to EC2 Flask app via `fetch()`
3. Flask receives and logs the data:
   - Name
   - Email
   - Message
4. Frontend displays success/failure message based on response

---

## 📁 Project Structure

```
project-root/
│
├── index.html              # Resume page with contact form
├── profile.jpg             # Profile image
└── app.py                  # Flask backend hosted on EC2
```

---

## 🧪 EC2 Setup Commands

```bash
sudo apt update
sudo apt install python3-pip -y
sudo apt install python3-full python3-venv -y
python3 -m venv myenv
source myenv/bin/activate
pip install flask flask-cors
python app.py
```

---

## 🐍 Flask Code (app.py)

```python
from flask import Flask, request, jsonify
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

@app.route('/contact', methods=['POST'])
def contact():
    data = request.json
    print(f"Name: {data['name']}, Email: {data['email']}, Message: {data['message']}")
    return jsonify({'status': 'success', 'message': 'Form received'}), 200

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---

## 🌐 Frontend Example (Fetch API)

```js
fetch("http://<ec2-public-ip>:5000/contact", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ name, email, message })
})
```

---

## 🔐 Security Group Rule

| Type       | Protocol | Port Range | Source       |
|------------|----------|------------|--------------|
| Custom TCP | TCP      | 5000       | 0.0.0.0/0    |

---

## 📦 Future Improvements

- Add HTTPS using API Gateway or SSL on EC2
- Save form submissions to DynamoDB or send via SES
- Add domain name via Route 53
- CI/CD pipeline with GitHub Actions

---

## 👤 Author

**Ritik Agrawal**  
📍 Mumbai, India  
📧 ritikagrawal2710@gmail.com  
🔗 [GitHub Profile](https://github.com/RitikAg2710)

---
