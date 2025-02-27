# 🚀 Spring Context Maven Archetype

Quickly bootstrap a **Spring Context** project with an **Uber-JAR**, pre-configured **Spring Beans**, and **Annotation Scanning**.

## 📌 Features
✅ **Pre-configured Spring Context** (no manual setup needed)  
✅ **Maven Shade Plugin** for easy **Uber-JAR generation**  
✅ **Pre-defined Beans & Config Setup**  
✅ **Annotation-based Component Scanning**  

---

# 📖 **Setup Guide**
This guide is **modular**, meaning you can **skip sections** if you've already configured your GitHub and Maven settings.

---

## ✅ **Step 1: Generate a GitHub Personal Access Token**
If you've already configured **GitHub authentication for Maven**, **skip this step**.

### **1️⃣ Generate a GitHub Personal Access Token**
1. Go to [GitHub → Developer Settings → Tokens](https://github.com/settings/tokens).
2. Click **"Generate new token (classic)"**.
3. **Select these permissions**:
   - ✅ `read:packages`
4. Click **Generate Token** and **copy** it.

---

## ✅ **Step 2: Configure Maven Authentication for GitHub**
If you've already configured **Maven to access GitHub Packages**, **skip this step**.

### **1️⃣ Store Your GitHub Credentials in `settings.xml`**
1. Open the Maven settings file:
   ```sh
   nano ~/.m2/settings.xml
   ```
2. Add the following inside `<settings>`:
   ```xml
   <servers>
       <server>
           <id>github</id>
           <username>YOUR_GITHUB_USER</username>
           <password>YOUR_GITHUB_TOKEN</password>
       </server>
   </servers>
   ```
   **Replace `YOUR_GITHUB_USER`** with your **GitHub Personal User**.
   **Replace `YOUR_GITHUB_TOKEN`** with your **GitHub Personal Access Token**.

3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

---

## ✅ **Step 3: Add the GitHub Repository for the Archetype**
If you've already configured this, **skip this step**.

1. Open `~/.m2/settings.xml` again:
   ```sh
   nano ~/.m2/settings.xml
   ```
2. Add the following under `<settings>`:
   ```xml
   <mirrors>
       <mirror>
           <id>github</id>
           <mirrorOf>github</mirrorOf>
           <url>https://maven.pkg.github.com/sebalooc-35/spring-context-archetype</url>
           <repositoryManager>true</repositoryManager>
       </mirror>
   </mirrors>

   <profiles>
       <profile>
           <id>github</id>
           <repositories>
               <repository>
                   <id>github</id>
                   <url>https://maven.pkg.github.com/sebalooc-35/spring-context-archetype</url>
                   <snapshots>
                       <enabled>true</enabled>
                   </snapshots>
               </repository>
           </repositories>
       </profile>
   </profiles>

   <activeProfiles>
       <activeProfile>github</activeProfile>
   </activeProfiles>
   ```
3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

---

## ✅ **Step 4: Use the Spring Context Archetype**
Now that your Maven is configured to use GitHub Packages, you can generate a new project using this archetype.

### **1️⃣ Run This Command to Create a New Project**
```sh
mvn archetype:generate \
    -DarchetypeGroupId=org.example \
    -DarchetypeArtifactId=spring-context-archetype \
    -DarchetypeVersion=1.0.1 \
    -DgroupId=com.mycompany \
    -DartifactId=my-spring-project \
    -DinteractiveMode=false
```

**Replace:**
- `com.mycompany` → The **group ID of your new project**.
- `my-spring-project` → The **name of the new project**.

---

## ✅ **Step 5: Build and Run the New Project**
### **1️⃣ Navigate to Your New Project**
```sh
cd my-spring-project
```

### **2️⃣ Build the Project**
```sh
mvn clean package
```

### **3️⃣ Run the Uber-JAR**
```sh
java -jar target/my-spring-project-1.0.0.jar
```

🚀 **Your Spring Context application should now be running!** 🎉

---

# **📌 Troubleshooting**
### ❓ **Getting Authentication Errors?**
- Double-check that your **GitHub token is correct** inside `settings.xml`.
- Ensure the **server ID is `github`** in both:
  - `<servers>`
  - `<distributionManagement>` (if needed).

### ❓ **Getting a "Could Not Resolve Archetype" Error?**
- Ensure your **GitHub repository URL** is correctly set inside `settings.xml`.
- Try running:
  ```sh
  mvn clean install
  ```
  to refresh local package data.

---

# 🎯 **Final Thoughts**
✅ **This guide is modular**—you can skip sections you’ve already configured.  
✅ **No more boilerplate**—just generate, build, and run!  
✅ **Now share your archetype and help others!** 🚀🔥

💬 **If you found this useful, let me know!** 😊

