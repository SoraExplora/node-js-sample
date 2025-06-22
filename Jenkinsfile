pipeline {
  agent any

  stages {
    stage('Checkout SCM') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test'
      }
    }

    stage('Code Analysis - SonarQube') {
      steps {
        withSonarQubeEnv('MySonarQube') {
          sh 'npx sonar-scanner'
        }
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t nodejs-app:latest .'
      }
    }

    stage('Push to Nexus (Optional)') {
      steps {
        echo 'Simulate uploading to Nexus or Docker Registry'
      }
    }

    stage('Deploy to Kubernetes') {
      steps {
        // Export the kubeconfig and check access, then deploy
        sh '''
          export KUBECONFIG=/var/lib/jenkins/.kube/config
          echo "Checking Kubernetes nodes:"
          kubectl get nodes
          echo "Applying deployment.yaml:"
          kubectl apply -f k8s/deployment.yaml
        '''
      }
    }
  }
}

