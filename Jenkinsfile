pipeline {
    agent any
    
    tools {
        maven 'system-maven' 
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/PJ2005/jenkins-demo'
            }
        }
        
        stage('Remove Python Files') {
            steps {
                echo 'Cleaning up existing Python files...'
                sh 'find . -name "*.py" -type f -delete'
            }
        }
        
        stage('Build Java Project') {
            steps {
                echo 'Building Java project with Maven...'
                sh 'mvn clean package'
            }
        }
        
        stage('Push Changes') {
            steps {
                echo 'Pushing updated workspace changes...'
                withCredentials([usernamePassword(credentialsId: 'github-push-token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh '''
                        git config user.name "Jenkins Build Agent"
                        git config user.email "jenkins@buildagent.local"
                        git add .
                        git commit -m "Chore: Automated removal of Python files [skip ci]" || echo "No changes to commit"
                        git push https://${GIT_USERNAME}:${GIT_PASSWORD}@://github.com/PJ2005/jenkins-demo HEAD:main
                    '''
                }
            }
        }
    }
}
