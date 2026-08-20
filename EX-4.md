# Ex.No 04 – Use the GAE Launcher to Launch Web Applications

## Aim
To use the Google App Engine (GAE) launcher / Google Cloud SDK to launch web applications.

## Tools Used
- Google Cloud Console
- Google Cloud SDK

## Procedure

1. **Create/select a project**: Create a new Cloud Console project, or retrieve the project ID of an existing one.
2. **Go to the project page** in the Google Cloud Console.
3. **Install and initialize** the Google Cloud SDK.
4. **Download the SDK** to your local machine.
5. **Create a website** to host on Google App Engine.

### Project Structure
```
project-id/
├── app.yaml       → App Engine configuration (URL routing to static files)
└── www/           → Static files (HTML, CSS, images, JS)
    ├── css/
    │   └── style.css
    ├── images/
    ├── js/
    └── index.html
```

### 6. Create `app.yaml`
The `app.yaml` file tells App Engine how to map URLs to static files:
```yaml
runtime: python27
api_version: 1
threadsafe: true

handlers:
- url: /
  static_files: www/index.html
  upload: www/index.html
- url: /(.*)
  static_files: www/\1
  upload: www/(.*)
```

### 7. Create `index.html`
Place this in the `www/` directory:
```html
<html>
<head>
<title>Hello, world!</title>
<link rel="stylesheet" type="text/css" href="/css/style.css">
</head>
<body>
<h1>Hello, world!</h1>
<p>This is a simple static HTML file that will be served from Google App Engine.</p>
</body>
</html>
```

### 8. Deploy the Application
Run from the root directory containing `app.yaml`:
```
gcloud app deploy
```
Optional flags:
- `--project [YOUR_PROJECT_ID]` — specify an alternate Cloud Console project ID
- `-v [YOUR_VERSION_ID]` — specify a version ID

### 9. View the Application
```
gcloud app browse
```
This launches the browser to view the deployed app at:
```
https://PROJECT_ID.REGION_ID.r.appspot.com
```

## Result
The GAE launcher (Google Cloud SDK) was used to successfully launch the web application.
