pipeline{
   agent any
   stages{
      stage('git_communication'){
         steps{
            git branch:"main",
               url:"https://github.com/dummyrepos/SampleWeb.git"
         }
      }
      stage('build and analysisi'){
         steps{
            withSonarQubeEnv(credentialsId: 'SONARCLOUD', installationName: 'SONAR_CLOUD'){
            sh "/var/lib/jenkins/.dotnet/tools/dotnet-sonarscanner begin /k:siadevops_dotnet-samaple /o:siadevops /d:sonar.token=56b31a9dafb3da3d26322d9bf80735a57fc4c2d5"
            sh "dotnet build SampleMVC.sln --no-incremental"
            sh 'dotnet test SampleMVC.sln'
            sh 'dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/'
            sh '/var/lib/jenkins/.dotnet/tools/dotnet-sonarscanner end /d:sonar.token=56b31a9dafb3da3d26322d9bf80735a57fc4c2d5'
            }
         }

      }
   }
}