# Jenkins Basics for QA Engineers

Jenkins is a CI server you run yourself.
GitHub Actions is easier for individuals.
Jenkins is what you will encounter in enterprise teams.

---

## What Jenkins Does

Watches your repository for changes.
When you push code, Jenkins runs your test suite automatically.
Sends email or Slack notification on failure.
Stores test reports and artifacts.

---

## Key Concepts

| Term | Meaning |
|------|---------|
| Job | A configured task (run tests, build app) |
| Build | One execution of a job |
| Pipeline | A multi-stage job defined in code |
| Jenkinsfile | The file that defines a pipeline |
| Agent | The machine that runs the job |
| Stage | A logical section of a pipeline (Test, Deploy) |
| Step | A single command within a stage |

---

## A Basic Jenkinsfile

Create `Jenkinsfile` in your repo root:

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    pytest tests/ -v \
                        --tb=short \
                        --html=reports/report.html \
                        --self-contained-html
                '''
            }
        }

        stage('Publish Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    reportDir: 'reports',
                    reportFiles: 'report.html',
                    reportName: 'Test Report'
                ])
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'reports/*.html'
        }
        failure {
            echo 'Tests failed — notify team'
        }
        success {
            echo 'All tests passed'
        }
    }
}
```

---

## GitHub Actions vs Jenkins

| | GitHub Actions | Jenkins |
|---|---|---|
| Hosting | Cloud (GitHub) | Self-hosted |
| Cost | Free for public repos | Free but needs a server |
| Setup | Minutes | Hours |
| Where used | Startups, open source | Enterprises |
| Config file | `.github/workflows/*.yml` | `Jenkinsfile` |
| Plugins | Limited | 1800+ plugins |

---

## Environment Variables in Jenkins

```groovy
environment {
    BASE_URL = 'https://staging.example.com'
    API_KEY  = credentials('api-key-secret')   // from Jenkins credentials store
}
```

Never hardcode credentials in `Jenkinsfile`.
Use Jenkins Credentials Manager for secrets.

---

## Triggering Builds

```groovy
triggers {
    // Every push via GitHub webhook
    githubPush()

    // Scheduled — every day at 2 AM
    cron('0 2 * * *')

    // Poll SCM every 5 minutes
    pollSCM('H/5 * * * *')
}
```
