# jenkins-installation-on-kubernetes-with-persistent-volume

**kubectl create namespace jenkins**

**vi deploy.yaml**

apiVersion: apps/v1
kind: Deployment
metadata:
  name: jenkins
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  template:
    metadata:
      labels:
        app: jenkins
    spec:
      containers:
      - name: jenkins
        image: jenkins/jenkins:lts-jdk11
        ports:
        - containerPort: 8080
        volumeMounts:
        - name: jenkins-home
          mountPath: /var/jenkins_home
      volumes:
      - name: jenkins-home
        emptyDir: {}
~

**vi sevice.yaml**

apiVersion: v1
kind: Service
metadata:
  name: jenkins
spec:
  type: NodePort
  ports:
  - port: 8080
    targetPort: 8080

  selector:
    app: jenkins
~
~
**kubectl apply -f . -n jenkins
kubectl get svc -n jenkins
kubectl get pods -n jenkins
kubectl describe svc -n jenkins
kubectl logs <> -n jenkins**
