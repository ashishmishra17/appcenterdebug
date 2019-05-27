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
  
  
I am at a loss. I have added all of the logs to the repository as well. Crash logs 11 are the logs after I removed the Pod file. 
The can be found in `./crashlogs`

  
