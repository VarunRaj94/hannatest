env.PATH = '/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Applications/Server.app/Contents/ServerRoot/usr/bin:/Applications/Server.app/Contents/ServerRoot/usr/sbin'
env.HOME = '/Users/iosbuilds'
env.USER = 'iosbuilds'
// backwards compat with old branch variable
env.GIT_BRANCH = env.BRANCH_NAME

def getWorkspace() {
    pwd().replace("%2F", "_")
}

def wipeWorkspace(String workspace) {
    if (workspace) {
        sh "find ${workspace} -mindepth 4 -depth -delete"
    }
}

def isRelease() {
    if (env.RELEASE == "true") {
      return true
    }
}

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

// Mark the code build 'stage'....
    //     stage 'Build'
    //     sh "security list-keychains -s ~/Library/Keychains/iosbuilds.keychain"
    //     sh "security unlock-keychain -p ${env.KEYCHAIN_PASSWORD} /Users/iosbuilds/Library/Keychains/iosbuilds.keychain"
      //   if (isRelease()) {
   //        sh "fastlane build_release"
   //      } else {
   //        sh "fastlane build_alpha"
    //     }
 // sh "fastlane scan"
         // Mark the code unit tests 'stage'....
         stage 'Tests'
         // reset the simulators before running tests
         sh "bundle exec fastlane tests" 
    }
}
