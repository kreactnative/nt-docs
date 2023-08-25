#### install velero (minio) 
#### client tools Macos
```
brew install velero
```
#### create credential credentials-velero
```
[default]
aws_access_key_id = minio
aws_secret_access_key = minio123
```
#### recheck secrer 
```
kubectl create secret generic cloud-credentials --from-file=credentials-velero -n velero
```
```
kubectl apply -f minio-deployment.yaml
```
#### install velero
```
velero install \
    --provider aws \
    --plugins velero/velero-plugin-for-aws:v1.2.1 \
    --bucket velero \
    --secret-file ./credentials-velero \
    --use-volume-snapshots=false \
    --backup-location-config region=minio,s3ForcePathStyle="true",s3Url=http://minio.velero.svc:9000
```
#### backup
```
velero backup create {{backup-name}}
velero backup describe  {{backup-name}}
```
#### copy pod backups file to local
```
kubectl -n velero cp {{minio podname}}:/storage /Users/dotnetnat/projects/temp/do-velero-backups/
```

#### copy backups file to kube pod
```
kubectl cp /Users/dotnetnat/projects/temp/do-velero-backups/velero/backups velero/minio-8649b94fb5-frjnm:/storage/velero/backups
```
#### restore (if diference env copy from backup)
```
velero restore create --from-backup {{backup-name}}
```
