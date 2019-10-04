proj_name_lc [headless] : Project Name Lower Case
proj_name_mc [Headless] : Project Name Mixed Case
proj_name_uc [HEADLESS] : Project Name Upper Case
proj_comment [Headless Chrome Example App] : Project Comment/Description
domain_name [cfapps.us10.hana.ondemand.com] : Domain Name (do not include hostname ex: conciletime.com use cfapps.xx##.hana.ondemand.com)
account_subdomain [conciletime] : Subdomain name specified in the CF subaccount
jenkins_git_creds [GITHUBALUNDESAP] : Jenkins Credentials Store Name for Git Repo
jenkins_cf_creds [CF_CREDENTIALSID] : Jenkins Credentials Store Name for Cloud Foundry Account
jenkins_cf_region [us10] : One of us10, us20, us30, eu10, etc.
jenkins_cf_org [ConcileTime] : Cloud Foundry organization for deployment
jenkins_cf_space [dev] : Cloud Foundry space for deployment
```
npm config set @sap:registry "https://npm.sap.com/" ; npm config set registry "https://registry.npmjs.org/" ; npm config set strict-ssl true
mkdir -p target
mta --build-target=CF --mtar=target/headless-CF.mtar build
```
