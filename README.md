**Task2: Microservices Architecture and Deployment**

1.  **Fork Repository**

<!-- -->

1.  <https://github.com/saleor/saleor-platform> repository which
    contains essential Docker Compose elements for configuring,
    building, and executing Saleor components.

<img src="./media/image1.png" style="width:6.26806in;height:2.46528in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image2.png" style="width:6.26806in;height:1.89306in"
alt="A screenshot of a computer Description automatically generated" />

2.  **Clone forked repository into local machine.**

<!-- -->

1)  Copy <https://github.com/SangayW/saleor-platform.git> and then below
    command in the local machine terminal.

- git clone <https://github.com/SangayW/saleor-platform.git>

> <img src="./media/image3.png" style="width:6.26806in;height:2.41875in"
> alt="A screenshot of a computer Description automatically generated" />

2)  Change directory to cloned directory.

- cd saleor-platform

3)  Build the application

- docker compose build

<img src="./media/image4.png"
style="width:5.09054in;height:0.49308in" />

4)  Apply Django migrations:

- docker compose run --rm api python3 manage.py migrate

<img src="./media/image5.png" style="width:4.97248in;height:6.00031in"
alt="A screenshot of a computer program Description automatically generated" />

5)  Populate the database with example data and create the admin user.

- docker compose run --rm api python3 manage.py populatedb
  –createsuperuser

<img src="./media/image6.png" style="width:6.26806in;height:1.60347in"
alt="A computer screen shot of a computer Description automatically generated" />

6)  Run the application

- docker compose up

7)  Results

- Saleor Core (API) - [http://localhost:8000](http://localhost:8000/)

<img src="./media/image7.png" style="width:6.26806in;height:2.49236in"
alt="A screenshot of a computer Description automatically generated" />

- Saleor Dashboard - [http://localhost:9000](http://localhost:9000/)

<img src="./media/image8.png" style="width:6.26806in;height:2.93264in"
alt="A screenshot of a computer Description automatically generated" />

- Jaeger UI (APM) - [http://localhost:16686](http://localhost:16686/)

<img src="./media/image9.png" style="width:6.26806in;height:2.40417in"
alt="A cartoon of a blue squirrel Description automatically generated" />

- Mailpit (Test email interface)
  - [http://localhost:8025](http://localhost:8025/)

<img src="./media/image10.png" style="width:5.94475in;height:2.70847in"
alt="A screenshot of a computer Description automatically generated" />

3.  Pushing the changes to the git i.e. chaned port number for Dashboard
    to 9003

<img src="./media/image11.png"
style="width:6.26806in;height:3.74028in" />

Note: PAT (Personal Access Token) is required while pushing updated code
to git using ubuntu terminal. Below snapshot shows the way to generate
PAT

1.  Go to **Settings** option under your profile.

<img src="./media/image12.png" style="width:6.26806in;height:4.29236in"
alt="A screenshot of a computer Description automatically generated" />

2.  Go to **Developer Settings**

<img src="./media/image13.png" style="width:6.26806in;height:3.69792in"
alt="A screenshot of a computer Description automatically generated" />

3.  Select **Personal Access Tokens** option under Developer Settings

<img src="./media/image14.png" style="width:6.26806in;height:1.35in"
alt="A screenshot of a computer Description automatically generated" />

4.  Generate by choosing the options given in the snapshot.

Note: Save the generated token in the text file to be used later.

<img src="./media/image15.png" style="width:6.26806in;height:2.25694in"
alt="A screenshot of a computer Description automatically generated" />

5.  Push the modified code to git

6.  Add tag to the project and push the tag to the git

- git tag -a isec6000-assignment1-task2 -m “tag for the task2 of
  assignment1”

- git push origin isec6000-assignment1-task2

<img src="./media/image16.png" style="width:5.86141in;height:1.52091in"
alt="A computer screen shot of a program Description automatically generated" />

Output after pushing code to the GitHub.

<img src="./media/image17.png" style="width:6.26806in;height:2.87847in"
alt="A screenshot of a computer Description automatically generated" />

**Deploying the project into the Kubernetes cluster created in the
task1.**

1.  Converting docker compose file to Kubernetes file.

- **Kompose** is the tool that helps to generate Kubernetes resource
  file from the docker compose file without having to write it manually.

- Follow installation instructions given at
  <https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes/>

<img src="./media/image18.png"
style="width:6.26806in;height:0.62847in" />

<img src="./media/image19.png"
style="width:6.09059in;height:0.65976in" />

<img src="./media/image20.png" style="width:6.26806in;height:3.93542in"
alt="A computer screen shot of text Description automatically generated" />

- Run below command after completing the translation:

  - kubectl apply -f
    api-service.yaml,backend-env-configmap.yaml,common-env-configmap.yaml,dashboard-deployment.yaml,dashboard-service.yaml,db-claim1-persistentvolumeclaim.yaml,db-deployment.yaml,db-service.yaml,jaeger-deployment.yaml,jaeger-service.yaml,mailpit-deployment.yaml,mailpit-service.yaml,redis-deployment.yaml,redis-service.yaml,saleor-backend-tier-networkpolicy.yaml,saleor-db-persistentvolumeclaim.yaml,saleor-media-persistentvolumeclaim.yaml,saleor-redis-persistentvolumeclaim.yaml,worker-deployment.yaml

- Check all the services, secrets and all related resources from the
  Kubernetes cluster that has been created in the task 1.

- Push updated code to git

<img src="./media/image21.png" style="width:6.26806in;height:1.39653in"
alt="A screenshot of a computer program Description automatically generated" />

- To access the service from the Internet, expose dashboard application
  to the Internet by changing Deployment type to LoadBalancer.

<img src="./media/image22.png" style="width:6.26806in;height:2.49931in"
alt="A screenshot of a computer Description automatically generated" />

<img src="./media/image23.png" style="width:6.26806in;height:3.24097in"
alt="A screenshot of a computer Description automatically generated" />
