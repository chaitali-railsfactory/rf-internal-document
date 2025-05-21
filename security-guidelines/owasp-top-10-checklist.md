# OWASP Top 10 Security Checklist

The **OWASP Top 10** is a standard awareness document for developers and web application security. It represents the most critical security risks to web applications.

This checklist is designed to help developers—especially freshers—understand what each risk is, why it matters, and how to mitigate it effectively.

---

## OWASP Top 10 Checklist

### 1. Broken Access Control  
**What if not used:** Users might access other users' data or perform admin-only actions.  
**Why we should use it:** To ensure users only do what they're allowed to.  
**How we can implement:**  
- Use role-based access control.  
- Validate user permissions on the backend (not just frontend).  
- Disable access to unauthorized URLs, API calls, and actions.  

---

### 2. Cryptographic Failures (Previously: Sensitive Data Exposure)  
**What if not used:** Hackers can read passwords, credit cards, or personal data if they get access.  
**Why we should use it:** To protect sensitive data from being leaked or stolen.  
**How we can implement:**  
- Always use HTTPS.  
- Encrypt sensitive data like passwords (use bcrypt or Argon2).  
- Don’t store sensitive data unless absolutely necessary.  

---

### 3. Injection (e.g., SQL, NoSQL, Command Injection)  
**What if not used:** Attackers can run malicious commands in your app (e.g., drop database).  
**Why we should use it:** To prevent attackers from changing your queries or commands.  
**How we can implement:**  
- Use parameterized queries (e.g., prepared statements).  
- Never trust user input – always validate or sanitize it.  
- Avoid building queries using string concatenation.  

---

### 4. Insecure Design  
**What if not used:** Even if code is secure, flaws in design can create big holes.  
**Why we should use it:** To make sure security is part of your system architecture, not just coding.  
**How we can implement:**  
- Design features with abuse cases in mind.  
- Use threat modeling and security reviews early in development.  
- Keep security as a non-negotiable requirement.  

---

### 5. Security Misconfiguration  
**What if not used:** Default settings can leave your app open to attack (e.g., admin:admin logins).  
**Why we should use it:** Misconfigured apps are low-hanging fruit for attackers.  
**How we can implement:**  
- Change default credentials and keys.  
- Disable unnecessary features or ports.  
- Keep software updated and patched.  

---

### 6. Vulnerable and Outdated Components  
**What if not used:** Your app might be running old code with known holes.  
**Why we should use it:** Attackers target old libraries with known issues.  
**How we can implement:**  
- Regularly update all frameworks and libraries.  
- Use tools like `npm audit`, `bundler-audit`, or OWASP Dependency-Check.  
- Subscribe to security advisories for your stack.  

---

### 7. Identification and Authentication Failures  
**What if not used:** Attackers can impersonate other users or bypass login.  
**Why we should use it:** Login and identity are critical gates in any app.  
**How we can implement:**  
- Use strong password rules and two-factor authentication (2FA).  
- Don’t use custom login systems unless absolutely necessary.  
- Use secure session tokens and rotate them regularly.  

---

### 8. Software and Data Integrity Failures  
**What if not used:** Attackers can inject malicious code into your system (e.g., fake updates).  
**Why we should use it:** To ensure the code and data haven't been tampered with.  
**How we can implement:**  
- Use signed packages and code integrity checks.  
- Implement CI/CD security checks.  
- Avoid downloading dependencies from unknown sources.  

---

### 9. Security Logging and Monitoring Failures  
**What if not used:** Attacks might go unnoticed until it's too late.  
**Why we should use it:** Early detection helps reduce damage.  
**How we can implement:**  
- Log important security events like logins and failures.  
- Monitor logs for unusual behavior.  
- Set up alerts and incident response processes.  

---

### 10. Server-Side Request Forgery (SSRF)  
**What if not used:** Attackers can make your server fetch internal or sensitive resources.  
**Why we should use it:** To prevent attackers from misusing server privileges.  
**How we can implement:**  
- Validate and whitelist all URLs the server can request.  
- Don’t let users control request destinations directly.  
- Block internal IP ranges in outbound calls when not needed.  

---

**Pro Tip:** Bookmark this checklist and revisit it during every web development project.
