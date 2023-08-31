pipeline {
  
  agent any

    stages{

      stage('CHeck Pull Request'){

        when{

             expression {

               return env.CHANGE_ID != null

            }

          }

        steps{

              echo "Successfully made the Pull Request"

          }

      }

     stage('Merge Pull Request'){

        // when {

        //         expression {

        //                   return env.CHANGE_TARGET == 'main' && env.CHANGE_SOURCE == 'dev'

        //           }  

        //       }

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
