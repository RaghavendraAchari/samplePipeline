pipeline {
agent any
environment {
dotnet = 'path\\to\\dotnet.exe'
}
stages {
stage ('Checkout') {
            steps {
                 git url: 'https://github.com/RaghavendraAchari/samplePipeline',branch: 'master'
            }
}
stage ('Restore PACKAGES') {     
         steps {
             bat "dotnet restore"
          }
        }

stage('Build') {
     steps {
            bat 'dotnet build --configuration Release'
      }
   }
   stage('Publish') {
     steps {
           bat 'dotnet publish App.csproj -c Release'
      }
   }

    stage('deploy') {
        steps {
        azureWebAppPublish azureCredentialsId: params.azure_cred_id,
            resourceGroup: "myResourceGroup", appName: "jenkinssample10x1", sourceDirectory: "bin/Release/netcoreapp3.1/publish/"
        }
    }

 }
}
