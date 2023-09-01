pipeline{
  agent any
//   environment {
//     GIT_CREDENTIALS = credentials('git_token') // Replace with your credential ID
//   }
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
    stage('Check Branch Changes') {
        when {
            expression {
                // Define the base branch you want to compare (e.g., 'main')
                def baseBranch = 'main'
                
                // Check for code changes between the base branch and the current PR branch
                def gitCmd = """git diff --name-only ${baseBranch}...HEAD"""
                def codeChanges = sh(script: gitCmd, returnStdout: true).trim()
                
                // Check if there are code changes
                return codeChanges != ''
            }
        }
        steps {
            echo "Changes detected in the current branch"
            // Add your additional steps for handling branch changes here
        }
    }
  }
}