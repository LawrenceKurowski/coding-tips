# Deploying react apps
## Locally

1. make the "build" folder with all pretty production-ready versions of files (these will be overwritten every time you run)
```bash
npm run build
```

2. (if not have)
```bash 
npm install -g serve 
```

3. Serve locally
```bash
serve -s build -l 8000
```