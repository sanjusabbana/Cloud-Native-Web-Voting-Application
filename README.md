# Cloud-Native-Web-Voting-Application
Cloud-Native Web Voting Application with kubernetes
This cloud-native web application is built using a mix of technologies. It's designed to be accessible to users via the internet, allowing them to vote for their preferred programming language out of six choices: C#, Python, JavaScript, Go, Java, and NodeJS.



# Technical stuff:

* Frontend: The frontend of this application is built using React and JavaScript. It provides a responsive and user-friendly interface for casting votes.

* Backend and API: The backend of this application is powered by Go (Golang). It serves as the API handling user voting requests. MongoDB is used as the database backend, configured with a replica set for data redundancy and high availability.

# Kubernetes Resources
To deploy and manage this application effectively, we leverage Kubernetes and a variety of its resources:

1. Namespace: Kubernetes namespaces are utilized to create isolated environments for different components of the application, ensuring separation and organization.

2. Secret: Kubernetes secrets store sensitive information, such as API keys or credentials, required by the application securely.

3. Deployment: Kubernetes deployments define how many instances of the application should run and provide instructions for updates and scaling.

4. Service: Kubernetes services ensure that users can access the application by directing incoming traffic to the appropriate instances.

5. StatefulSet: For components requiring statefulness, such as the MongoDB replica set, Kubernetes StatefulSets are employed to maintain order and unique identities.

5. PersistentVolume and PersistentVolumeClaim: These Kubernetes resources manage the storage required for the application, ensuring data persistence and scalability.

# Learning Opportunities
Creating and deploying this cloud-native web voting application with Kubernetes offers a valuable learning experience. Here are some key takeaways:

* Containerization: Gain hands-on experience with containerization technologies like Docker for packaging applications and their dependencies.

* Kubernetes Orchestration: Learn how to leverage Kubernetes to efficiently manage, deploy, and scale containerized applications in a production environment.

* Microservices Architecture: Explore the benefits and challenges of a microservices architecture, where the frontend and backend are decoupled and independently scalable.

* Database Replication: Understand how to set up and manage a MongoDB replica set for data redundancy and high availability.

* Security and Secrets Management: Learn best practices for securing sensitive information using Kubernetes secrets.

* Stateful Applications: Gain insights into the nuances of deploying stateful applications within a container orchestration environment.

* Persistent Storage: Understand how Kubernetes manages and provisions persistent storage for applications with state.

By working through this project, you'll develop a deeper understanding of cloud-native application development, containerization, Kubernetes, and the various technologies involved in building and deploying modern web applications.




# Create EKS cluster with NodeGroup (2 nodes of t2.medium instance type) Create EC2 Instance t2.micro (Optional)

## IAM role for ec2

{
	"Version": "2012-10-17",
	"Statement": [{
		"Effect": "Allow",
		"Action": [
			"eks:DescribeCluster",
			"eks:ListClusters",
			"eks:DescribeNodegroup",
			"eks:ListNodegroups",
			"eks:ListUpdates",
			"eks:AccessKubernetesApi"
		],
		"Resource": "*"
	}]
}

# Install Kubectl:

curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.24.11/2023-03-17/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo cp ./kubectl /usr/local/bin
export PATH=/usr/local/bin:$PATH

Install awscli:

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

Once the Cluster is ready run the command to set context:

aws eks update-kubeconfig --name EKS_CLUSTER_NAME --region us-west-2
To check the nodes in your cluster run

kubectl get nodes
If using EC2 and getting the "You must be logged in to the server (Unauthorized)" error, refer this: https://repost.aws/knowledge-center/eks-api-server-unauthorized-error

Clone the github repo

git clone https://github.com/N4si/K8s-voting-app.git
Create CloudChamp Namespace

kubectl create ns cloudchamp

kubectl config set-context --current --namespace cloudchamp
MONGO Database Setup

