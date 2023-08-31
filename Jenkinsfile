pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from your repository
                checkout scm
            }
        }
        
        stage('stage-a') {
            when {
                changeset ".*pull_request.*"
            }
            steps {
                // Execute stage-a tasks here
                echo "Running stage-a..."
            }
        }
        
        stage('stage-b') {
            when {
                expression { currentBuild.changeSets[0].commitMessage =~ /Merge pull request/ }
            }
            steps {
                // Execute stage-b tasks here
                echo "Running stage-b..."
            }
        }
    }
}

// pipeline{
//   agent any
//   stages{
//     stage('pull'){
//       when{
//         expression {
//           return env.CHANGE_ID != null
//         }
//       }
//       steps{
//         echo "Successfully detect Pull Request"
//       } 
//     }
//     stage('merge'){
//       when{
//         expression{
//           // def changes 
//           return env.CHANGE_TARGET == 'main'
//         }
//       }
//       steps{
//         echo "Changes detected in the current branch"
//         // script {
//         //   def changes = scm.changeset()
//         //   if (changes) {
//         //     echo "Changes detected in the repository"
//         //   } else {
//         //     echo "No changes detected in the repository"
//         //     currentBuild.result = 'SUCCESS'  // Skip this stage if no changes
//         //   }
//         // }
//       } 
//     }
//   }
// }