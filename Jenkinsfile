node {
    echo "Started build $currentBuild.number" + "."
    stage('Import'){
    git 'https://github.com/will93hump/project2_v2.git'
    }
    
    try{
    stage('Analyze'){
        dir('DebateApp/DebateApp.Client'){
        bat '"C:\\Program Files\\dotnet\\dotnet.exe" restore'
        bat 'C:\\Tools\\SonarQube\\Scanner\\sonar-scanner-msbuild-3.0.2.656\\sonarqube.scanner.msbuild.exe begin /n:"DebateApp" /k:"dapp"'
        bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\BuildTools\\MSBuild\\15.0\\Bin\\msbuild.exe" DebateApp.Client.csproj /t:rebuild'
        bat 'C:\\Tools\\SonarQube\\Scanner\\sonar-scanner-msbuild-3.0.2.656\\sonarqube.scanner.msbuild.exe end'
        }
    }
    }
	
/*		dir('DebateApp/DebateApp.db'){
		bat '"C:\\Program Files\\dotnet\\dotnet.exe" restore'
        bat 'C:\\Tools\\SonarQube\\Scanner\\sonar-scanner-msbuild-3.0.2.656\\sonarqube.scanner.msbuild.exe begin /n:"DebateApp" /k:"dapp"'
        bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\BuildTools\\MSBuild\\15.0\\Bin\\msbuild.exe" DebateApp.db.csproj /t:rebuild'
        bat 'C:\\Tools\\SonarQube\\Scanner\\sonar-scanner-msbuild-3.0.2.656\\sonarqube.scanner.msbuild.exe end'
		}
		dir('DebateApp/DebateApp.Domain'){
		bat '"C:\\Program Files\\dotnet\\dotnet.exe" restore'
        bat 'C:\\Tools\\SonarQube\\Scanner\\sonar-scanner-msbuild-3.0.2.656\\sonarqube.scanner.msbuild.exe begin /n:"DebateApp" /k:"dapp"'
        bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\BuildTools\\MSBuild\\15.0\\Bin\\msbuild.exe" DebateApp.Domain.csproj /t:rebuild'
        bat 'C:\\Tools\\SonarQube\\Scanner\\sonar-scanner-msbuild-3.0.2.656\\sonarqube.scanner.msbuild.exe end'
		}
		dir('DebateApp/DebateApp.test'){
		bat '"C:\\Program Files\\dotnet\\dotnet.exe" restore'
        bat 'C:\\Tools\\SonarQube\\Scanner\\sonar-scanner-msbuild-3.0.2.656\\sonarqube.scanner.msbuild.exe begin /n:"DebateApp" /k:"dapp"'
        bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\BuildTools\\MSBuild\\15.0\\Bin\\msbuild.exe" DebateApp.db.csproj /t:rebuild'
        bat 'C:\\Tools\\SonarQube\\Scanner\\sonar-scanner-msbuild-3.0.2.656\\sonarqube.scanner.msbuild.exe end'
		}

		echo 'Code analysis stage complete.' 
		}
    catch(Exception e) {echo 'Code analysis stage failed:' + e}
    }

 */


    try{
        stage('Deploy'){
            dir('DebateApp/DebateApp.Client'){
                bat '"C:\\Program Files\\dotnet\\dotnet.exe" build /p:DeployOnBuild=true /p:PublishProfile=publish'
                bat '"C:\\Program Files (x86)\\IIS\\Microsoft Web Deploy V3\\msdeploy.exe" -verb:sync -source:iisApp="C:\\Program Files (x86)\\Jenkins\\workspace\\DebateApp\\DebateApp\\DebateApp.Client\\obj\\Debug\\netcoreapp2.0\\PubTmp\\Out" -dest:iisApp="Default Web Site/DebateApp",computerName="https://ec2-18-221-110-13.us-east-2.compute.amazonaws.com:8172/msdeploy.axd",userName="Administrator",password=Ybwo4.HWnpLnGnH.;CFkG*@I7ZWLKQOt,authType="Basic"  -enableRule:AppOffline -allowUntrusted'
            }      
        }
        currentBuild.result = 'SUCCESS'
    echo 'Deploy Stage:' + $currentBuild.result
    }
    catch(Exception e)
    {
        currentBuild.result = 'FAILURE'
        echo 'Deploy Stage:' + $currentBuild.result
    }
    

