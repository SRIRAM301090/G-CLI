node {
    
stage 'Checkout'
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '971d4d17-6a91-4d53-8e1d-66051cd122d5', url: 'ssh://git@github.com/JamesMc86/LabVIEW-CLI.git']]])

stage 'VS Build'
    //clean packages directory until this is removed from the repo
    bat 'del /f /s /q \"C Sharp Source/LabVIEW CLI/packages\" 1>nul'
    bat 'rmdir /s /q \"C Sharp Source/LabVIEW CLI/packages\"'
    bat 'nuget restore \"C Sharp Source/LabVIEW CLI/LabVIEW CLI.sln\"'
    bat "\"${tool 'MS Build'}\" \"C Sharp Source/LabVIEW CLI/LabVIEW CLI.sln\" /p:Configuration=Release /p:Platform=\"Any CPU\""
    
stage 'Integration Test'
    bat 'pushd \"Integration Tests\" & \"Run Integration Tests.bat\" \"../C Sharp Source/LabVIEW CLI/bin/Release/" & popd'

}