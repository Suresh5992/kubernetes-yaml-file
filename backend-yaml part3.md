#django-backend

apiVersion: apps/v1  //API version for Deployment.
kind: Deployment  // Deployments, StatefulSets, DaemonSets, etc.
metadata:  // giving details for deployment for reference  as name and lables 
  name: django-backend
spec:  //  what deployment need to do work 
  replicas: 1   // means only one pod will be running
  selector:  // Selector defines how the Deployment finds which pods it manages.
    matchLabels:  //It looks for pods with label app: django-backend. This must match the labels on pod templates.
      app: django
  template:  // for pod create down hare || The template describes the pods that will be created. || for pod Reference
    metadata:  //The pod template has its own metadata with labels. Here, pods created by this Deployment will have the label app: django, matching the selector above.
      labels:
        app: django
    spec: // what pod need to do work 
      containers:   //container is defined with the name django-backend.
        - name: django
          image: madeep2669/django-backend:14 // Docker ECR or any : 14 means Version 
          ports:
            - containerPort: 8000   // network ports the container exposes.internally
          resources:  //resource requests and limits for the container.
            requests:
              cpu: "100m"
              memory: "128Mi"
            limits:
              cpu: "500m"
              memory: "256Mi"
          env:   // environment variables inside the container. // *** Connect to Database  *****   
            - name: SECRET_KEY  // seperate secrets.yaml in which Database username and passwd is there 
              valueFrom: // secrets.yaml we need to right this apps/v1 how it can't change like this 
                secretKeyRef:  //secrets.yaml we need to right this apps/v1 how it can't change like this 
                  name: django-secrets    // seperate secrets.yaml in which Database username  
                  key: SECRET_KEY  // seperate secrets.yaml in which Database  passwd 
            - name: DEBUG  //This enables debug mode in Django. Shows detailed errors in the browser. 📌 Useful in development — not safe in production.
              value: "True" //This enables debug mode in Django. Shows detailed errors in the browser. 📌 Useful in development — not safe in production.
            - name: ALLOWED_HOSTS //Allows requests from any domain/IP.📌 "*" means “allow all”.In production, use: "example.com"
              value: "*" //Allows requests from any domain/IP.📌 "*" means “allow all”.In production, use: "example.com"
            - name: DB_NAME  //Name of the MySQL database that Django should connect to.
              value: "django_database" //Name of the MySQL database that Django should connect to.
            - name: DB_USER //The username for MySQL login
              value: "root"  //The username for MySQL login
            - name: DB_PASSWORD  //Securely gets password from a Kubernetes Secret (called django-secrets).
              valueFrom:  //Securely gets password from a Kubernetes Secret (called django-secrets).
                secretKeyRef:  //Securely gets password from a Kubernetes Secret (called django-secrets).
                  name: django-secrets  //Securely gets password from a Kubernetes Secret (called django-secrets).
                  key: DB_PASSWORD  //Securely gets password from a Kubernetes Secret (called django-secrets).
            - name: DB_HOST  // Hostname (usually the service name of MySQL in Kubernetes).
              value: "mysql-django"  Hostname (usually the service name of MySQL in Kubernetes).
            - name: DB_PORT  //MySQL default port number. --> Port used to connect to MySQL.
              value: "3306"  //MySQL default port number. --> Port used to connect to MySQL.
---
apiVersion: v1
kind: Service 
metadata:  / giving details for service  for reference  as name and lables  ** he name of the service is django-service. This is how other pods (like frontend or DB) can access it inside the cluster.
  name: django-service
spec:  // what service need to do work 
  type: ClusterIP  //This service is only accessible inside the cluster (internal).📌 Other options: NodePort, LoadBalancer.
  selector: // Selector defines how the service finds which pods it manages.
    app: django
  ports:
    - port: 8000
      targetPort: 8000
      
      
      
      🖼️ Visual Flow:
      
      User (Frontend Pod)
    |
    |  Request to → django-service:8000
    |
Service (ClusterIP)
    |
    |  Forwards to → Pod with label: app: django
    |                      at port 8000
    ↓
Django Backend Container



🔍 Explanation – Line by Line: 


| Line                                                   | Explanation                                                                                                                                                                                                        |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `apiVersion: v1`                                       | Using core v1 API version in Kubernetes.                                                                                                                                                                           |
| `kind: Service`                                        | You are creating a **Service** object (used to expose a Pod).                                                                                                                                                      |
| `metadata:`<br>`  name: django-service`                | The name of the service is `django-service`. This is how other pods (like frontend or DB) can **access it** inside the cluster.                                                                                    |
| `spec:`                                                | Starting the configuration part.                                                                                                                                                                                   |
| `type: ClusterIP`                                      | This service is **only accessible inside the cluster** (internal).<br>📌 Other options: `NodePort`, `LoadBalancer`.                                                                                                |
| `selector:`<br>`  app: django`                         | This service **routes traffic** to pods that have the label `app: django`.<br>📌 Must match your **Deployment** labels.                                                                                            |
| `ports:`<br>`  - port: 8000`<br>`    targetPort: 8000` | - `port`: the **port** this service exposes.<br> - `targetPort`: the **port inside the container**.<br><br>📌 Traffic coming to service on port `8000` will be **forwarded** to port `8000` inside the Django pod. |










