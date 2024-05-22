pipeline{
  agent any
  stages{
    stage('Build'){
      steps{
        echo "Etapa build no disponible"
      }
    }
    stage ('Tests'){
      steps{
        echo "Etapa tests no disponible"
      }
    }
    stage ('Deploy'){
      steps{
        sh "docker-compose down -v"
      }
    }
  }
}