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
         sh 'git branch'
      } 
    }
    stage('Check Branch Changes') {
        when {
            expression {
                // Define the target branch you want to compare (e.g., 'main')
                def targetBranch = 'main'
                
                // Update remote references to fetch the latest changes from the target branch
                sh "git fetch origin ${targetBranch}:${targetBranch}"
                
                // Check for code changes between the current branch and the target branch
                def gitCmd = """git diff --name-only ${targetBranch}...HEAD"""
                def codeChanges = sh(script: gitCmd, returnStdout: true).trim()
                
                // Check if there are code changes
                return codeChanges != ''
            }
        }
        steps {
            echo "Changes detected in the current branch"
            sh 'git branch'
            // Add your additional steps for handling branch changes here
        }
    }
  }
}