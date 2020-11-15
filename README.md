# NPFMMK
mysql
# 1. add repo
helm repo add bitnami https://charts.bitnami.com/bitnami
# 2. install 
helm install laravel-database  --set mysqlRootPassword=rootpassword,mysqlUser=homestead,mysqlPassword=secret,mysqlDatabase=laravel,persistence.existingClaim=mysql-pvc bitnami/mysql 

minio
# 1. add repo
helm repo add minio https://helm.min.io/
# 2. install
helm install minio --set accessKey=TCI4823FJXBK0206GOXX,secretKey=xHC90qBeyZW04r+4bWf8gOn2pYGlFhfLzgcotBGn minio/minio

# 1. apply configMap for nginx configuration
kubectl apply -f configMap.yaml
# 2. apply persistent volume shared between nginx and php-fpm pods
kubectl apply -f volumes/
# 3. apply deployment
kubectl apply -f  k8s-nginx-php-fpm-deployment.yaml
# 3. apply expose deployment
kubectl expose deployment web --type=NodePort --name=web-service
kubectl describe service/web-service
# 4. show service
kubectl get services
# 5. port show
minikube service web-service --url
