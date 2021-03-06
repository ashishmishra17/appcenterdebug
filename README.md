# appcenterdebug
debugging cocopods repo for appcenter support

With another project I have been having issues getting a succesful build once I added coco-pods.
This project is to walk through a simple from scratch project so AppCenter support has enough info to help
trouble shoot the problem. I believe, not that the problem is systemic. 

So Here is a walkthrough of what was done for this project. 
You can check out any commits and run locally on you own machine
1. `react-native init debugproject`
2. open Xcode and run project created - success
3. Create repository
4. add repository to the project `git init` and then `git remote add origin git@github.com:ahujsak/appcenterdebug.git`
5. commit and push init project
6. create new project in appcenter
7. link project to git repo (have not installed appcenter sdk) 
8. set up build for initial commit with legacy build selected on
9. build is successful
10. followed instructions for adding appecenter sdk
  * `npm install appcenter appcenter-analytics appcenter-crashes --save-exact`
  * Deleted package-lock.json
  * `rm -rf node_modules`
  * `yarn`
  * `react-native link`
  * open Xcode with workspace -> build
  * success
11. Commit and build on appcenter
  * clang error
  * I read on help site, to reopen the build settings and to save and build again
  * turned off legacy build
  * buid -> success
12. Added provisioning profile to app center as well as correct certificate
  * Build _> fail 
13. Guessing it was a conflict with bundle id, changed bundle id in Xcode and committed 
  * build -> fail 
14. Turned off credentials to not sign the build
  * build -> fail
15. Added correct credentials to Xcode to match bundle id.
  * build locally -> success
  * commit and build -> fail 
16. Added back signing credentials to appcenter 
  * build -> fail
17. After initial response from support ticket over the weekend, I removed the Pods file from git
  * build -> fail
18. After interaction with Support, and lookin at the logs to compare, a key difference is in legacy build system vs new
19. I switech to legacy build system 
    * build -> success
    * So I tried the same thing in my other project and failed. 
    * so now I am going to add the rest of the pods to this project and see if there is a problem
20. added pods for basic react native and did pod update
    Installing DoubleConversion (1.1.6)
    Installing Folly (2018.10.22.00)
    Installing React (0.59.8)
    Installing boost-for-react-native (1.63.0)
    Installing glog (0.3.5)
    Installing yoga (0.59.8.React)
21. Local Build succcessful commit to appcennter
    * build -> failed.
    * The only change was to the pod file adding the above pods
    * check the logs in `./crashlogs/logs_16/` 
    * The following build commands failed:
    `Ld /Users/vsts/Library/Developer/Xcode/DerivedData/debugproject-frhbfcerhsbogmexcwddmwbbbhpn/Build/Intermediates.noindex/ArchiveIntermediates/debugproject/IntermediateBuildFilesPath/debugproject.build/Release-iphoneos/debugproject.build/Objects-normal/armv7/debugproject normal armv7`
22.  followed support suggestion and read and followed article https://intercom.help/appcenter/build/ios/my-ios-builds-fail-with-clang-error-linker-command-failed-with-exit-code-1
    * build failed again
    * added logs to folder 18 in crash logs. 
    * this is the failed command `he following build commands failed:
	`Ld /Users/vsts/Library/Developer/Xcode/DerivedData/debugproject-frhbfcerhsbogmexcwddmwbbbhpn/Build/Intermediates.noindex/ArchiveIntermediates/debugproject/IntermediateBuildFilesPath/debugproject.build/Release-iphoneos/debugproject.build/Objects-normal/armv7/debugproject normal armv7 (1 failure)` THere is no clang error there. 
  
  
I am at a loss. I have added all of the logs to the repository as well. Crash logs 11 are the logs after I removed the Pod file. 
The can be found in `./crashlogs`

  
