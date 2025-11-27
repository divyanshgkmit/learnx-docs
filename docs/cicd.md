### **1. Create Feature Branch**
Create branch from `dev` branch.

**Naming:**
```
feature/<feature-name>
```

**Example:**
```
feature/course-progress
```

### **2. Implement Feature**
Write code, test locally, commit changes.

**Commit:**
```bash
git commit -m "feat: add progress tracking"
```

### **3. Push to GitHub**
```bash
git push origin feature/<feature-name>
```

### **4. Create Pull Request**
PR from `feature/` → `develop`

### **5. Code Review**
Review for security, quality, performance.

### **6. Approval & Merge**
Merge to `develop` after approval.

### **7. Production Release**
PR `develop` → `main`

### **8. Deployment**
- **Frontend:** Vercel
- **Backend:** AWS EC2


