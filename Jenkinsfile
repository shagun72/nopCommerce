pipeline {
    agent { label 'dot' }
    options {
        timeout(time: 1, unit: 'HOURS')
                                                 
    }
    triggers {
        pollSCM('* * * * *')
    tools{
        dotnetsdk 'DOTNET8'
    }    
    }
    stages {
        stage('SCM') {
            steps { 
                git url: 'https://github.com/shagun72/nopCommerce.git' ,
                    branch: 'develop'
            }
        }
        stage('BUILD') {
            steps {
                sh 'dotnet build --configuration Release src/Presentation/Nop.Web/Nop.Web.csproj'
                sh ' dotnet publish src/Presentation/Nop.Web/Nop.Web.csproj --configuration Release --output published'
            }
        
            post {
                success {
                    zip zipFile: './published.zip',
                    archive: true,
                    dir: './published'
                }
            }      
        }
    }

}