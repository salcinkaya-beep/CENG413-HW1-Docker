Requires Docker; run these commands from the project folder.
Build: `docker build -t selin-web:1.0 .`
Run: `docker run -d --name selin-web -p 8080:8080 -e APP_MESSAGE="Hello from Selin's Docker app" selin-web:1.0`
Check: `curl http://localhost:8080/health`
Other endpoints: http://localhost:8080/ and http://localhost:8080/info
