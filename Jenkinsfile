node {
    stage('Checkout/Build/Test') {
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
        // Build and Test
        sh 'xcodebuild -workspace MaterialDesign.xcworkspace -scheme "MaterialDesign" -configuration "Debug" build test -destination "platform=iOS Simulator,name=iPhone 6,OS=11.2" -enableCodeCoverage YES | /usr/local/bin/ocunit2junit' 
        // Publish test restults.
        step([$class: 'JUnitResultArchiver', allowEmptyResults: true, testResults: 'build/reports/junit.xml'])
    }
}