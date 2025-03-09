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

## ✅ **Step 2: Ensure You Have a `settings.xml` File**
Maven uses `settings.xml` to store configuration (including credentials). This file is typically located at `~/.m2/settings.xml`.

1. **Check if `~/.m2/settings.xml` exists**:

   ```sh
   ls ~/.m2/settings.xml
   ```
2. If it **does not exist**, create one:
   ```sh
   nano ~/.m2/settings.xml
   ```
   Paste in the following **skeleton** to start:
   ```xml
   <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
       <!-- You will add servers, mirrors, profiles, etc. here -->
   </settings>
   ```
3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).

---

## ✅ **Step 3: Configure Maven Authentication for GitHub**
If you've already configured **Maven to access GitHub Packages**, **skip this step**.

### **1️⃣ Store Your GitHub Credentials in `settings.xml`**
1. Open your `settings.xml`:
   ```sh
   nano ~/.m2/settings.xml
   ```
2. Inside `<settings> ... </settings>`, add the `<servers>` block:
   ```xml
   <servers>
       <server>
           <id>github</id>
           <username>YOUR_GITHUB_USER</username>
           <password>YOUR_GITHUB_TOKEN</password>
       </server>
   </servers>
   ```
   Replace `YOUR_GITHUB_USER` with your **GitHub username**, and `YOUR_GITHUB_TOKEN` with your **Personal Access Token**.

3. Save and exit (`CTRL + X`, then `Y`, then `Enter`).



---

## ✅ **Step 4: Add the GitHub Repository for the Archetype**
If you've already done this, **skip**.

1. Open `~/.m2/settings.xml` again:

   ```sh
   nano ~/.m2/settings.xml
   ```
2. **Inside** the `<settings>` block, add these sections:
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

## ✅ **Step 5: Use the Spring Context Archetype**
Now that your Maven is configured to use GitHub Packages, you can generate a new project using this archetype.

### **1️⃣ Run This Command to Create a New Project**
```sh
mvn archetype:generate \
    -DarchetypeGroupId=org.example \
    -DarchetypeArtifactId=spring-context-archetype \
    -DarchetypeVersion=1.0.2 \
    -DgroupId=com.mycompany \
    -DartifactId=my-spring-project \
    -DinteractiveMode=false
```
Replace:
- `com.mycompany` → **group ID** for your new project.
- `my-spring-project` → **artifact ID** or name of the new project.

---

## ✅ **Step 6: Build and Run Your New Project**
1. **Navigate** to your newly created project:
   ```sh
   cd my-spring-project
   ```
2. **Build** the project:
   ```sh
   mvn clean package
   ```
3. **Run** the Uber-JAR:
   ```sh
   java -jar target/my-spring-project-1.0.0.jar
   ```
   You should see your **Spring Context** application start up successfully! 🎉

---

# **📌 Troubleshooting**
### ❓ **Authentication Errors?**
- Double-check that your **GitHub token** is correct inside `settings.xml`.
- Make sure the `<server>` `id` matches `github` in both `<servers>` and `<mirrors>`/`<repositories>` sections.

### ❓ **Could Not Resolve Archetype?**
- Confirm the `<url>` to GitHub Packages is correct.
- Try:
  ```sh
  mvn clean install
  ```
  to refresh local repo data.

---
That’s it! If you follow these steps, you should be able to generate a fresh Spring Context project via your Maven archetype.

Enjoy your new Spring project!
