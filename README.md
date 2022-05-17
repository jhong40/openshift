# openshift
```
minishift.exe start --vm-driver virtualbox
minishift.exe oc-env
oc login -u system:admin
oc whoami
oc get users
oc get projects
oc adm policy add-cluster-role-to-user cluster-admin administrator
```

```
oc whoami
  system:admin
oc login -u developer -p developer
oc new-project myproject   # create new proj
oc project myproject       # change to proj
oc get pv --as system:admin



```

+ https://livebook.manning.com/book/openshift-in-action/oc-cheat-sheet/
+ https://github.com/nekop/openshift-sandbox/blob/master/docs/command-cheatsheet.md
