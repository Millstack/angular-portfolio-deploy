
# Git Build Settings

## AWS Amplify setting location:

`AWS Amplify` - `app_name` - `Hosting` (left side) - `Build Settings` - `amplify.yml` file

## 1. Amplify Bild code for git repo only
```yml
version: 1
frontend:
    phases:
        preBuild:
            commands:
                - 'npm ci'
        build:
            commands:
                - 'npm run build'
    artifacts:
        baseDirectory: dist/angular-portfolio/browser
        files:
            - '**/*'
    cache:
        paths:
            - 'node_modules/**/*'

```


## 2. Amplify Bild code for git repo having submodule
```yml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - git config --global url."https://${GITHUB_PAT}@github.com/".insteadOf "https://github.com/"
        - git submodule update --init --recursive
        - cd app-source && npm install
    build:
      commands:
        - cd app-source && npm run build
  artifacts:
    baseDirectory: app-source/dist/angular-portfolio/browser
    files:
      - "**/*"
  cache:
    paths:
      - app-source/node_modules/**/*
```
