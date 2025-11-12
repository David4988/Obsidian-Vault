	[[Maven Wrapper]]
### Maven Lifecycle Phases:

1. **`clean`** – removes temporary directories and build artifacts
    
2. **`default`** – the core build lifecycle (compile → package → install → deploy)
    
3. **`site`** – generates documentation and project reports
    

> ⚙️ A **phase** can contain one or more **goals**.

---

### 1. **Clean Lifecycle**

|Phase|Description|
|---|---|
|`pre-clean`|Pre-cleaning hook, runs before `clean`|
|`clean`|Deletes `target/` and temp files|
|`post-clean`|Post-cleaning hook, runs after `clean`|

---

### 2. **Default (Build) Lifecycle**

This is the **main lifecycle**, used to build your project.

|Phase|Description|
|---|---|
|`validate`|Validates the project structure and configuration|
|`compile`|Compiles source code|
|`test`|Runs unit tests|
|`package`|Packages code into a JAR/WAR|
|`verify`|Runs integration tests or verification|
|`install`|Installs the package to the local repository|
|`deploy`|Deploys the package to a remote repository|

> 💡 Running a phase also runs **all previous phases** in order.
> 
> Example: `mvn install` executes: `validate → compile → test → package → verify → install`

---

### 3. **Site Lifecycle**

Used for generating documentation and project reports.

|Phase|Description|
|---|---|
|`pre-site`|Prepares before generating the site|
|`site`|Generates project documentation (HTML, reports, etc.)|
|`post-site`|Executes after site generation|
|`site-deploy`|Deploys site to a server (e.g., GitHub Pages, WebDAV)|

---