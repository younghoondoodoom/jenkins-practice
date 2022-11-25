pipline {
  agent any

  triggers {
    pollSCM('*/3 * * * *')
  }

  environment {
    AWS_ACCESS_KEY_ID = credentials('awsAccessKeyId')
    AWS_SECRET_ACCESS_KEY = credentials('awsSecretAccessKey')
    AWS_DEFAULT_REGION = 'ap-northeast-2'
  }

  stages {
    stage('Prepare') {
      agent any

      steps {
        echo "Lets start Long Journey!"
        echo 'Clonning Repository'

        git url: 'https://github.com/younghoondoodoom/jenkins-practice.git',
            branch: 'master'
            credentialsId: 'gittest'
      }

      post {
        success {
          echo 'Successfully Cloned Repository'
        }

        always {
          echo "i tried..."
        }

        cleanup {
          echo "after all other post condition"
        }
      }
    }

    stage('Build') {
      steps {
          echo  '빌드를 시작합니다.'

          sh './gradlew clean build'
      }

      post {
        success {
          echo '빌드 성공!'
        }

        failure {
          echo '빌드 실패!'
        }
      }
    }

    stage('Test') {
      steps {
        echo  '테스트를 시작합니다.'

        sh './gradlew test'
      }

      post {
        success {
          echo '테스트 성공!'
        }

        failure {
          echo '테스트 실패!'
        }
      }
    }

    stage('Deploy') {
      steps {
        echo  '배포를 시작합니다.'

        sh './gradlew run'
      }

      post {
        success {
          echo '배포 성공!'
        }

        failure {
          echo '배포 실패!'
        }
      }
    }

  }

}
