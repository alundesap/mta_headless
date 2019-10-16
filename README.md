```
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
```
npm config set @sap:registry "https://npm.sap.com/" ; npm config set registry "https://registry.npmjs.org/" ; npm config set strict-ssl true
mkdir -p target
mta --build-target CF --mtar target/headless-CF.mtar build
```

```
git add . ; git commit -m "atomic commit" ; git push
```


First create the services ahead of the deploys.
This is because for some reason the deploy from local files which picks up the mtad.yaml file munges the path to be xs-securityjson and fails.
```
cf create-service xsuaa application CONCILE_UAA -c ./xs-security.json
cf create-service hana securestore CONCILE_SS
```

Now do a local deploy which uses the mtad.yaml file and creates the module from a docker container and binds the services to it.
```
cf deploy .
```

Now build the rest of the app to an mtar per the mta.yaml file (note doesn't include the docker based module.)
```
mta --build-target CF --mtar target/headless-CF.mtar build
```

Finally deploy the mtar file but skip the ownership check since otherwise it will complain that the UAA is already associated with the concile-headless mta and won't let the headless mta also bind to it.
```
cf deploy target/headless-CF.mtar --skip-ownership-validation

```
