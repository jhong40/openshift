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
oc Cheat Sheet
oc is the primary command line for OpenShift. It includes tools to build, deploy, and administer containers.

Logging in

oc login -u=<username> -p=<password> --server=<your-openshift-server> --insecure-skip-tls-verify
copy
Switch to a specific project or log in directly to a project:

1
2
oc project <myproject>
oc login -n <myproject>
copy
Building and deploying applications

Build code or a Dockerfile in a Git repo:

oc new-app centos/ruby-22-centos7~https://github.com/openshift/ruby-ex.git
copy
Build from a template:

oc new-app --template=myproject/mytemplate -p=<param_name>=<param_value>
copy
Create other objects from a file:

oc create -f myobject.yaml -n <myproject>
copy
Update an existing object:

oc patch svc mysvc --type merge --patch '{"spec":{"ports":[{"port": 8080, "targetPort": 5000 }]}}'
copy
Accessing running applications

1
2
3
oc exec <mypod> cat /opt/app-root/myapp.config
oc rsh <mypod
oc debug dc <mydc>
copy
Common commands

1
2
3
4
5
6
7
8
oc status
oc logs pod <mypod>
oc get pods --all-namespaces
oc describe pod <mypod>
oc get services --sort-by=.metadata.name
oc delete all -l app=tomcat
oc delete pod <mypod> --grace-period=0
oc export bc,dc,is,svc --as-template=myapp.yaml
copy
Scaling applications

1
2
oc scale dc <mydc> --replicas=5
oc autoscale dc/app-cli --min 2 --max 5 --cpu-percent=75
copy
Administrative operations using the adm subcommand

Manage user roles:

1
2
3
oc adm policy add-role-to-user admin oia -n python
oc adm policy add-cluster-role-to-user cluster-reader system:serviceaccount:monitoring:default
oc adm policy add-scc-to-user anyuid -z default
copy
Manage node state:

oc adm manage node <node> --schedulable=false
copy
Run cluster diagnostics:

oc adm diagnostics
copy
Advanced operations

Create a config map file and mount it as a volume to a deployment config:

1
2
3
oc create configmap propsfilecm --from-file=application.properties
oc set volumes dc/myapp --add --overwrite=true --name=configmap-volume
 --mount-path=/data -t configmap --configmap-name=propsfilecm
copy
Create a secret from the CLI and mount it as a volume to a deployment config:

1
2
3
4
oc create secret generic oia-secret --from-literal=username=myuser
 --from-literal=password=mypassword
oc set volumes dc/myapp --add --name=secret-volume --mount-path=/opt/app-root/
 --secret-name=oia-secret
copy

