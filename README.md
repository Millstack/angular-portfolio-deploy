
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
        # 1. Initialize the submodule to fetch your angular-portfolio code
        - git submodule update --init --recursive
        # 2. Enter the app-source folder to install dependencies
        - cd app-source && npm install
    build:
      commands:
        # 3. Build the project from within the submodule directory
        - cd app-source && npm run build
  artifacts:
    # 4. Point to the build output located inside the submodule folder
    baseDirectory: app-source/dist/angular-portfolio/browser
    files:
      - '**/*'
  cache:
    paths:
      - app-source/node_modules/**/*
```
