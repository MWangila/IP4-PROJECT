pipeline { 
  agent any 
  tools{

  nodejs 'NodeJS-16.13.2'

  }

  stages { 
    stage('clone repository') {
      steps { 
        
         // Get some code from a GitHub repository
                git 'https://github.com/MWangila/IP4-PROJECT'
      }
    }
     stage('Build the project') {
      steps { 
        sh 'echo "here we will Build" '
      }
    }
stage('Install Dependencies') {
      steps { 
        sh 'npm install'
      }
    }
		stage('Tests') {
      steps { 
        sh 'npm test'
      }
    }
    repositories {
  mavenCentral()
}

dependencies {
  // your dependencies
}

sourceSets {
  main {
    java {
      srcDirs = ['src/main/java']
    }
    resources {
      srcDirs = ['src/main/resources']
    }
  }
}
    stage('Deploy Application') {
      steps {
               withCredentials([usernameColonPassword(credentialsId: 'heroku_jenkins', variable: 'HEROKU_CREDENTIALS' )]){

                    sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/ip4herokuconn.git master'
              }
    }
  }
}
}