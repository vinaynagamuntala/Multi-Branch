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
        sh 'git checkout dev'
        def currentBranch = sh(returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
        echo "Current branch: ${currentBranch}"
        sh 'git branch'
      } 
    }
    stage('Check Branch Changes') {
        when {
            expression {
                 // Check if there are any changes in the 'main' branch
                def changes = checkout(
                    scm: [$class: 'GitSCM',
                        branches: [[name: 'main']], // Specify the branch name here
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [],
                        submoduleCfg: [],
                        userRemoteConfigs: [[url: 'https://github.com/vinaynagamuntala/Multi-Branch.git']]] // Replace 'your-repo-url' with your actual repository URL
                    )
                    return changes
            }
        }
        steps {
            echo "Changes detected in the current branch"
            def currentBranch = sh(returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
            echo "Current branch: ${currentBranch}"
            sh 'git branch'
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