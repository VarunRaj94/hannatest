node {
    stage('Checkout') {
        // Checkout files.
        checkout([
            $class: 'GitSCM',
            branches: [[name: 'master']],
            doGenerateSubmoduleConfigurations: false,
            extensions: [], submoduleCfg: [],
            userRemoteConfigs: [[
                name: 'hannatest',
                url: 'https://github.com/VarunRaj94/hannatest.git/'
            ]]
        ])
	}

    stage('Build') {
        sh 'xcodebuild -workspace MaterialDesign.xcworkspace -scheme "MaterialDesign" -configuration "Debug" build test -destination "platform=iOS Simulator,name=iPhone 6,OS=11.2" -enableCodeCoverage YES | /usr/local/bin/ocunit2junit' 
    }

    stage('Test') {
        step([$class: 'JUnitResultArchiver', allowEmptyResults: true, testResults: 'test-reports/*.xml'])
    }	

    stage('Code Coverage') {
	sh '/usr/local/bin/slather coverage --jenkins --html --scheme MaterialDesign MaterialDesign.xcworkspace/'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html', reportFiles: 'index.html', reportName: 'Coverage Report'])
    }

//sh 'xcodebuild -workspace MaterialDesign.xcworkspace -scheme "MaterialDesign" -configuration "Release" clean archive -archivePath /Users/apple/Desktop DEVELOPMENT_TEAM=A79T4B24DZ'

}
