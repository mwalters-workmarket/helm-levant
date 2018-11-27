Set-up:
Install helm:
* Download from https://storage.googleapis.com/kubernetes-helm/helm-v2.11.0-darwin-amd64.tar.gz
* `mv helm /usr/local/bin`
* `helm init --client-only`

From parent folder, execute `helm template permissions-service` to render the template, you'll notice it fails because some fields are required,
so try `helm template permissions-service -f env-config/dev-permissions-values.yaml --set database.read.user=a,database.write.user=b,database.read.password=c,database.write.password=d`

Now render the umbrella chart `helm template permissions-service-umbrella -f env-config/dev-permissions-umbrella-values.yaml`

Another way of expressing a dependencies is rather than using a pure umbrella chart, like above,
your chart can have a conditional requirement.
Look at permissions-service-2/requirements.yaml
acl is only included if 'deployAcl' is true
