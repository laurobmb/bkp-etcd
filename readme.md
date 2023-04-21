# ETCD backup from Openshift 4.12

https://access.redhat.com/solutions/5843611

## Install Kustomization.yaml
oc apply -k kustomization.yaml

## Execute before apply yamls
oc adm policy add-scc-to-user privileged -z openshift-backup
oc adm policy add-scc-to-user privileged system:serviceaccount:openshift-etcd-backup:openshift-backup

## Create job for test
oc -n openshift-etcd-backup create job backup --from=cronjob/openshift-backup

## Uninstall Kustomization.yaml
oc delete -k kustomization.yaml