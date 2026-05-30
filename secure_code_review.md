# Secure Coding Review & Source Code Audit Report[cite: 1]

## 1. Vulnerable Code Analysis (Python/Flask Target)
The following code snippet presents a critical **SQL Injection (SQLi)** vulnerability due to improper input sanitization and dynamic query construction[cite: 1]:

```python
# VULNERABLE FUNCTION
@app.route('/login', methods=['POST'])
def login():
    username = request.form['username']
    password = request.form['password']
    
    # Flaw: Direct string formatting incorporates untrusted input into the SQL execution engine
    query = "SELECT * FROM users WHERE username = '%s' AND password = '%s'" % (username, password)
    cursor.execute(query)
    user = cursor.fetchone()