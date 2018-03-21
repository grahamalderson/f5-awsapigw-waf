# f5-awsapigw-waf
Postman collection and environment to quickly deploy WAF protection in front of AWS API Gateway onto an existing F5 BIG-IP.

More information here:
https://devcentral.f5.com/articles/protect-your-aws-api-gateway-with-f5-big-ip-waf-30667

To get the tests to function you will need to install the f5-postman-workflows framework into Postman:

1. Open Postman
2. Click the ‘Import’ button
3. Select ‘Import from Link’
4. Enter https://raw.githubusercontent.com/0xHiteshPatel/f5-postman-workflows/master/F5_Postman_Workflows.postman_collection.json in the field
5. Click the ‘Import’ button
6. Navigate to your Postman Collections
7. Expand the ‘F5_Postman_Workflows’ collection
8. Expand the ‘Install’ folder
9. Click the ‘Install/Upgrade f5-postman-workflows’ items
10. Click the ‘Send’ button
11. Verify the installation was successful by:
12. Examine the response tests and ensure the ‘Install Successful’ test passed
13. Examine your Postman Global Environment and look for a _f5_workflow_functions item populated with JavaScript code

You can download and import this collection and environment, fill in the required variables, and it will do all the work for you in a few seconds. You can take it a step farther and automate deployment and configuration of the BIG-IP in AWS if you want, but this simple collection assumes you already have a BIG-IP deployed and have assigned an IP that you want to use. You’ll import the collection and the environment. Open up the environment and set the variables noted below.

You’ll need to fill in the relevant environment variables. Here’s a quick set of definitions:

bigip_username: your username
bigip_password: your password
bigip_mgmt: management IP of your BIG-IP, use the elastic IP pointing to the management interface so you can reach it
monitor_receive_string: a string you expect to receive to indicate success at the below URI
monitor_uri: the URI you want to monitor, remember that the AWS Api GW stage name will prefix it like /
app_dnsname: the FQDN you will point at the BIG-IP, in the below example I’m using “my-desired-fqdn.com”
aws_apigateway_dnsname: the DNS name used by AWS API gateway for your API
app_ip: the IP you want to use for the virtual server to receive traffic, this is a secondary IP assigned to your traffic network interface
app_name: This will be used as a prefix in the name for all objects created so you can easily identify them
cert_name: You can leave this as “default.crt” for a self-signed or select an SSL certificate uploaded to the BIG-IP
key_name: You can leave this as “default.key” for a self-signed or select an SSL key you uploaded to the BIG-IP

Note

If you’re using a single NIC, you’ll need to alter the calls because they assume your management runs on 443, and you’ll be running management on 8443. Also, you then use 0.0.0.0/0 for the virtual server (app_ip). Remember that if you’re deploying behind the API Gateway you don’t need to do a rewrite and can modify the calls accordingly and a few of the variables won’t be used.
