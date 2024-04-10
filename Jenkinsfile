pipeline {
    agent {
        label 'my-label1-&&-my-label_jdk_17'
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('scm') {
            steps {
                git url: 'https://github.com/dummyrepos/nopCommerceApr24.git',
                    branch: 'develop'
            }
        }
        stage('build') {
            steps {
                sh 'dotnet publish -o published/ -c Release src/Presentation/Nop.Web/Nop.Web.csproj'        
            }
       
            post {
                failure {
                    mail bcc: 'all@learningthoughts.io',
                        from: 'jenkins@learningthouths.io',
                        to: "dev@learningthoughs.io",
                        subject: "Build of ${JOB_BASE_NAME} with Build Id ${BUILD_ID} is failed",
                        body: "Refer to ${RUN_DISPLAY_URL} for more info"

                }
                success {
                    mail bcc: 'all@learningthoughts.io',
                        from: 'jenkins@learningthouths.io',
                        to: "dev@learningthoughs.io",
                        subject: "Build of ${JOB_BASE_NAME} with Build Id ${BUILD_ID} is success",
                        body: "Refer to ${RUN_DISPLAY_URL} for more info"
                }
            }  
        }
    }
}