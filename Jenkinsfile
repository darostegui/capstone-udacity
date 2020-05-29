pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e green/*.html blue/*.html'
      }
    }

    stage('Build Blue & Green Docker Image') {
      steps {
        withCredentials(bindings: [[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]) {
          sh '''
						docker build -t globalint/capstoneblue -f blue/Dockerfile .
            docker build -t globalint/capstonegreen -f green/Dockerfile .
					'''
        }

      }
    }

    stage('Push Image(s) To Dockerhub') {
      steps {
        withCredentials(bindings: [[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD']]) {
          sh '''
						docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
						docker push globalint/capstoneblue
            docker push globalint/capstonegreen
					'''
        }

      }
    }

    stage('Set current kubectl context') {
      steps {
        withAWS(region: 'us-east-1', credentials: 'aws-static') {
          sh '''
						kubectl config use-context arn:aws:eks:us-east-1:837633013847:cluster/thecluster
					'''
        }

      }
    }

    stage('Deploy blue container') {
      steps {
        withAWS(region: 'us-east-1', credentials: 'aws-static') {
          sh '''
						kubectl apply -f ./blue-controller.json
					'''
        }

      }
    }

    stage('Deploy green container') {
      steps {
        withAWS(region: 'us-east-1', credentials: 'aws-static') {
          sh '''
						kubectl apply -f ./green-controller.json
					'''
        }

      }
    }

    stage('Create the service in the cluster, redirect to blue') {
      steps {
        withAWS(region: 'us-east-1', credentials: 'aws-static') {
          sh '''
						kubectl apply -f ./blue-service.json
					'''
        }

      }
    }

    stage('Wait user approve') {
      steps {
        input 'Ready to redirect traffic to green?'
      }
    }

    stage('Create the service in the cluster, redirect to green') {
      steps {
        withAWS(region: 'us-east-1', credentials: 'aws-static') {
          sh '''
						kubectl apply -f ./green-service.json
					'''
        }

      }
    }

  }
}
