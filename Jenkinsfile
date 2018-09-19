pipeline{
      agent  { node { label 'master' } }
      environment
      {
        SOLUTION_NAME = 'creditservice.sln'
        BUILD_NUMBER = '1.0.1'
        PROJECT_NAME = 'creditservice.csproj'
        NUSPEC = 'CoreBanking.App.nuspec'
        PROJECT_TEST_NAME = 'creditservice.Test'
      }
    stages
    {
        stage('prepare')
        {
            steps
            {
                echo  "setup the app environment...."                    
            }      
        }
        stage('clone')
        {
            steps
            {
                echo "echo cloning the  repository..."
                checkout scm
            }      
        }
        stage('build')
        {
            steps
            {
                echo "building the app..."
                sh "dotnet restore ${SOLUTION_NAME}"
                    script 
                    {                        
                        sh "dotnet build ${SOLUTION_NAME}"
                    } 
            }
        
        }
        stage('unit test')
        {
            steps
            {
                sh "dotnet test ${PROJECT_TEST_NAME} -v n"
            }
        
        }
        stage('quality')
        {
            steps
            {
                echo "running sonarqube...."
            }
        
        }
        stage('SAST')
        {
            steps
            {
                echo "running fortify..."
            }      
        }
        stage('package')
        {
            steps
            {             
                echo "packaging the app to NUGET..."
                sh "dotnet pack -o publish ./creditservice/${PROJECT_NAME}"            
              //  sh 'dotnet nuget push ./publish/creditservice.1.0.1.nupkg -s https://pipepper.pkgs.visualstudio.com/_packaging/Pipackagernet/nuget/v3/index.json -k h2gkcbe2ru6vnmf3lpb5gfpm5wfev2qm4oc6yigzklohubllmm5a'
            }    
        }
        stage('publish')
        {
            steps
            {
                echo "publishing the app using Terraform..."             
            }       
        }
    }
}