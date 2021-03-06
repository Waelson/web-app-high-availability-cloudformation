# High Availability to Web Application on AWS
Template to create high availability infrastructure for web application on AWS Cloudformation.
<br/>
<h4>How to use:</h4>
Before you begin to use this repository, check you have installed AWS CLI in your machine. If you haven't installed it, please consider to visit <a href="https://docs.aws.amazon.com/cli/latest/userguide/install-bundle.html">AWS CLI Site</a> for more informations.
<br/><br/>
<ul>
  <li>Into repository, you will find two shell scripts files to create and update stack on Cloudformation. Use them to manipulate your Cloudformation stack or as reference to learn about Cloudformation commands using AWS CLI. </li>
  <li>Create stack: <code>./create.sh &#60;your-stack-name&#62; &#60;cloudformation-script-yml-file&#62; &#60;parameter-file&#62;</code></li>
  <li>Update stack: <code>./update.sh &#60;your-stack-name&#62; &#60;cloudformation-script-yml-file&#62; &#60;parameter-file&#62;</code></li>
  <li>Note #1: Scripts must to be executed according to the following order: First, <code>networks.yml</code> responsable for creation all network configurations and last <code>servers.yml</code> to create EC2 instances and other resources associated to them.</li>
  <li>Note #2: If you need to change IP range, check <code>network-params.json</code> file to update configurations.</li>
  <li>Note #3: You will need to create a Key Pair through web console, to edit <code>servers.yml</code> file and to update value of the KeyName attribute in the resource AWS::AutoScaling::LaunchConfiguration.</li>
</ul>

<h4>Main points architecture:</h4>
<ul>.
  <li>All single points of failure were eliminated. Remember, resources like Internet Gateway and Load Balancer are managed by AWS team.</li>
  <li>Redundancy was included by Auto Scaling Group and Database Replication.</li>
  <li>All resources  are distributed between two availability zones. So, we guarantee more availability to architecture.</li>
  <li>All EC2 instances are accessible just via load balancer. Note that all instances belong to private subnet, isolating them of all external traffic.</li>  
  <li>Important Note: Script files don't create database. Therefore, I recommend you to create database through web console (RDS - Relational Database Service) and associate it to your private subnet.</li>
</ul>
<h4>Solution diagram:</h4>
<img src="https://github.com/Waelson/web-app-high-availability-cloudformation/blob/master/Diagram-CloudFormation.png">


