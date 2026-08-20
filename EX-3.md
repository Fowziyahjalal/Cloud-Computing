# Ex.No 03 – Install Google App Engine (Hello World App)

## Aim
To install Google App Engine and create a "Hello World" app and other simple web applications using Python/Java.

## Tools Used
- Eclipse IDE
- Google Plugin for Eclipse
- Google App Engine (GAE) Java SDK

## Procedure

### 1. Install Google Plugin for Eclipse
Install the Google Plugin for Eclipse. If the Google App Engine Java SDK was installed together with the plugin, skip to step 2 — otherwise, download the GAE Java SDK separately and extract it.

### 2. Create a New Web Application Project
1. In the Eclipse toolbar, click the **Google** icon and select **New Web Application Project…**
2. In the project wizard:
   - **Project name**: `HelloWorld`
   - **Package**: e.g. `com.mkyong`
   - Deselect **Use Google Web Toolkit**
   - Check **Use Google App Engine** and configure the SDK
3. Click **Finish** — Eclipse generates a sample project automatically.

### 3. Review the Generated Project
Standard Java web project structure:
```
HelloWorld/
├── src/            → Java source code
│   └── META-INF/   → other configuration
└── war/            → JSPs, images, data files
    └── WEB-INF/    → app configuration
        ├── lib/     → JARs for libraries
        └── classes/ → compiled classes
```

The key file is `appengine-web.xml`, which App Engine needs to run and deploy the application:
```xml
<?xml version="1.0" encoding="utf-8"?>
<appengine-web-app xmlns="http://appengine.google.com/ns/1.0">
  <application></application>
  <version>1</version>
  <system-properties>
    <property name="java.util.logging.config.file" value="WEB-INF/logging.properties"/>
  </system-properties>
</appengine-web-app>
```

### 4. Run It Locally
1. Right-click the project → **Run As** → **Web Application**.
2. Eclipse console shows:
   ```
   INFO: The server is running at http://localhost:8888/
   INFO: The admin console is running at http://localhost:8888/_ah/admin
   ```
3. Open `http://localhost:8888/` to see "Hello App Engine!" with available servlets listed.
4. Open `http://localhost:8888/helloworld` to see the servlet output: `Hello, world`.

### 5. Deploy to Google App Engine
1. Register an account at https://appengine.google.com/ and create an application ID (e.g., `mkyong123`).
2. Add the ID to `appengine-web.xml`:
   ```xml
   <application>mkyong123</application>
   ```
3. Click the **GAE deploy** button in the Eclipse toolbar → **Deploy to App Engine…**
4. Sign in with your Google account and click **Deploy**.
5. Once deployed, the app is available at `http://mkyong123.appspot.com/`.

## Result
Google App Engine was installed successfully, and a "Hello World" web application was developed and deployed on GAE.
