0. Install IoTEdge Custom Resource Definition (CRD): `helm install --repo https://edgek8s.blob.core.windows.net/staging edge-crd edge-kubernetes-crd`  
1. Create Kubernetes Namespace : `kubectl apply -f https://raw.githubusercontent.com/jaypaddy/iotedgek8s/main/ns.yaml`
2. Create Persistent Volume Claim : `kubectl apply -f https://raw.githubusercontent.com/jaypaddy/iotedgek8s/main/pvciotedged.yaml`
3. Create IoTEdge in IoTHub and copy Connection String
4. Store ConnString in a shell variable: `export connStr='<IoT Edge Device Connection String>'`
5. Install IoTEdge on Kubernetes 

helm install --repo https://edgek8s.blob.core.windows.net/staging pv-iotedged-example edge-kubernetes \ <br>
  --namespace pv-iotedged \ <br>
  --set "iotedged.data.persistentVolumeClaim.name=iotedged-data-azurefile" \ <br>
  --set "provisioning.deviceConnectionString=$connStr" 
  
  

#### Resiliency for EdgeAgent and EdgeHub
1. Create Persistent Volume Claim edgeAgent: `kubectl apply -f https://raw.githubusercontent.com/jaypaddy/iotedgek8s/main/pvcedgeagent.yaml`
2. Create Persistent Volume Claim edgeHub: `kubectl apply -f https://raw.githubusercontent.com/jaypaddy/iotedgek8s/main/pvcedgehub.yaml`


