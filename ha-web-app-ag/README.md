## Udacity High-Availability Website

### Prerequisites before running the CloudFormation scripts
1. The AWS user used for running the scripts must have permission to assign roles to resources, e.g. IAMFullAccess
2. A role for granting EC2 instances read-only access to S3 buckets must be already present in the AWS account. Default name of the role is "UdacityS3ReadOnlyEC2" but can be changed by setting the parameter "S3ReadOnlyRoleName" in the file "server-parameter.json"
3. The developer's ZIP file containing the web app is called "udacity-starter-website.zip". It must be uploaded to an S3 bucket of the AWS account. The full S3 path to the file is defined by setting the value of the parameter "S3PathToDeveloperZipFile" in the file "server-parameter.json"

### Running the scripts
Step 1 Setting up the network infrastructure

    ./create.sh AWSWebAppNetwork network.yml network-parameters.json

Step 2 Setting up the server infrastructure
    
    ./create.sh AWSWebAppServers servers.yml server-parameters.json
The URL of the Udagram website is an output of the stack, e.g. http://awswe-webap-7ec6rbsn7yd0-192815467.us-west-2.elb.amazonaws.com/ (not active anymore)

### Note
I'm also including file "servers2.yml". The difference to "servers.yml" is that it creates the role "UdacityS3ReadOnlyEC2" automatically. So that prerequisite 2 is no longer necessary, the resource "S3ReadOnlyRoleForEC2" is defined. Creation of the stack is successful. Alas, deletion of the stack fails with an error: the role cannot be deleted because there is still an instance profile associated with it. I've searched the AWS documentation and the web all over but I could not find a solution for this glitch. If you get the chance, it would be great if you could give me some pointers. Thanks!
