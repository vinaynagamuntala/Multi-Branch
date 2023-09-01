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
                // Check if there are any changes in the current branch
                // def changes = changeset branch: main
                // Check if there are any changes in the 'main' branch
                withCredentials([gitUsernamePassword(credentialsId: 'git_token', gitToolName: 'Default')]) {
                    def changes = checkout(
                        scm: [
                            $class: 'GitSCM',
                            branches: [[name: 'main']],
                            userRemoteConfigs: [[url: 'https://github.com/vinaynagamuntala/Multi-Branch.git']],
                            extensions: [[$class: 'CleanBeforeCheckout'], [$class: 'CloneOption', noTags: false, shallow: false]],
                        ]
                    )
                    return changes
                }
            }
        }
        steps {
            echo "Changes detected in the current branch"
            // Add your additional steps for handling branch changes here
        }
    }
  }
}

// pipeline {
//     agent any
    
//     stages {
//         stage('Checkout') {
//             steps {
//                 // Checkout the source code from your repository
//                 checkout scm
//             }
//         }
        
//         stage('stage-a') {
//             when {
//                 changeset ".*pull_request.*"
//             }
//             steps {
//                 // Execute stage-a tasks here
//                 echo "Running stage-a..."
//             }
//         }
        
//         stage('stage-b') {
//             when {
//                 expression { 
//                     def changeSets = currentBuild.changeSets
//                     return changeSets != null && changeSets.size() > 0 && changeSets[0].commitMessage =~ /Merge pull request/
//                 }
//             }
//             steps {
//                 // Execute stage-b tasks here
//                 echo "Running stage-b..."
//             }
//         }
//     }
// }

// when {
//     branch 'production'
// }
