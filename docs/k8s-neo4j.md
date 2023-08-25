#### install single 
```
helm upgrade --install neo4j-community equinor-charts/neo4j-community --set acceptLicenseAgreement=yes --set neo4jPassword=NT123### --namespace dbs --create-namespace
```