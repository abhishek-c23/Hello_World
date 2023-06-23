pipeline {
    agent { label "agentA" }
    
    triggers {
        pollSCM('* * * * *')
    }    

    stages {
        stage('clone_Hello_World_Project') {
            steps {
                echo 'clone Hello_World_Project'
                git 'https://github.com/abhishek-c23/Hello_World.git'
            }
        }
        stage('build_Hello_World_Project') {
            steps {
                echo 'build_Hello_World_Project'
                sh 'yum install maven -y'
                sh 'mvn -Dmaven.test.failure.ignore=true install'
            }
        } 
        stage('Docker_build') {
            steps {
                echo 'Docker build_Hello_World_Project'
                sh 'docker build -t hello_world_project .' 
            }
        }
        stage('login to dockerhub') {
            steps {
                echo 'login to dockerhub'
                sh 'docker login -u abhishekc23 -p abhi'
            }
        } 
        stage('Tag the Image') {
            steps {
                echo 'Tag the Image'
                sh 'docker tag  hello_world_project abhishekc23/hello_world_project'
            }
        } 
        stage('Deploy to docker hub') {
            steps {
                echo 'Deploy to docker hub'
                sh 'abhishekc23/hello_world_project'
            }
        }
        stage('Remove Docker conatiner') {
            steps {
                echo 'Remove Docker conatiner'
                sh 'docker stop projectd_conatiner || true'
                sh 'docker rm projectdconatiner || true'
            }
        }        
        stage('Run docker image') {
            steps {
                echo 'Deploy to docker hub'
                sh 'docker run --name projectd_conatiner -d -p 8181:8080 vnom1985/projectd'
            }
        }        
    }
}
