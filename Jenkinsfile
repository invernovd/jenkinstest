node {
       deleteDir()

       MAGENTO_DIR='magento'
       DEPLOY_DIR='deploy'

       branchInfo = getBranch()

       try {
              stage ('Clone') {
                     checkout scm
              }

              stage ('Artifact') {


                     if (branchInfo.type == 'master'){
                            sh "echo Artifact Master"
                     }
                     if (branchInfo.type == 'pre'){
                            sh "echo Artifact PRE"
                     }
              }

              stage ('Deploy') {
                     if (branchInfo.type == 'master'){
                            sh "echo Deploy Master"
                     }
                     if (branchInfo.type == 'pre'){
                            sh "Deploy PRE"
                     }
              }

              stage ('Clean Up') {
                     deleteDir()
              }
       } catch (err) {
              currentBuild.result = 'FAILED'
              throw err
       }
}

def getBranch() {
       def branch = [:]
       branchData = BRANCH_NAME.split('/')
       if (branchData.size() == 2) {
              branch['type'] = branchData[0]
              branch['version'] = branchData[1]
       } else {
              branch['type'] = BRANCH_NAME
              branch['version'] = BRANCH_NAME
       }
       return branch
}