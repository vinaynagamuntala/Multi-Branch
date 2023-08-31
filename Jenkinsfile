pipeline{
  agent any
  stages{
    stage('pull'){
      when{
        expression {
          return env.CHANGE_ID != null
        }
      }
      steps{
        echo "Successfully detect Pull Request"
      } 
    }
    stage('merge'){
      steps{
        script {
          def changes = scm.changeset()
          if (changes) {
            echo "Changes detected in the repository"
          } else {
            echo "No changes detected in the repository"
            currentBuild.result = 'SUCCESS'  // Skip this stage if no changes
          }
        }
      } 
    }
  }
}