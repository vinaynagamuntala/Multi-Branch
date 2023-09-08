pipeline{
  agent any
  stages{
    stage('git checkout') {
      steps{
        sh "rm -rf *"
        sh "git clone https://github.com/vinaynagamuntala/Multi-Branch.git"
      }
    }
    stage('Terraform plan'){
      when{
        expression {
          return env.CHANGE_ID != null
        }
      }
      steps{
        echo "Successfully detect Pull Request"
        sh 'git checkout dev'
        sh 'git branch'
      } 
    }
    stage('Terraform apply') {
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
            sh 'git checkout main'
            sh 'git branch'
            // Add your additional steps for handling branch changes here
        }
    }
  }
}