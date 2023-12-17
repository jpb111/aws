### To configure AWS CLI with a different profile name and add an access key, you can use

```Shell

aws configure --profile <your_profile_name>

```

### To list users

```Shell

aws iam list-users --profile <your_profile_name>

```

### I am Roles for AWS Services

### Basic code to start and EC2 apache server

```bash
#!/bin/bash
# Install httpd

yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f) </h1>" > /var/www/html/index.html

```

## Classic Ports

22 = SSH log into a linux instance
21 = FTP file transfer protocol
22 = SFTP Secure file transfer protocol
80 = HTTP - access unsecured websites
443 = HTTPS - Secure websites
3389 = Remote login windows instance

### Time out Error

Must be a security group issue

### SSH to an EC@ instance

Down the the private key, change permission

````bash

chmod 400 <keyName>

```bash

Now ssh into the ec2 instance

```bash
ssh -i <keyName> ec2-user@<PublicIpAddress>

````

## EC2 Instances Purchasing options

1. On Demand : pay by second
2. Reserved (Reservation Period: 1 & 3 years) : Up tp 72 percent discount to On demand, Payment option - No Upfront, partial upfront, All upfront, Usaually steady state applications. If you do not use it you can sell it in market place.
3. Savings plan ( 1 & 3 years ): 72 percent discount, commit a certain usage (for example $10 every month for 1 or 3 years, Usage beyond on Demand price )
4. Spot Instances: short world loads, cheap,
5. Dedicated Hosts ( book an entire physical server ): Most expensive option, Purchase option: on Demand and Reserved, When you have a software with your own licencse, no hardware share. Use of phycial server
6. Dedicated instances: May share hardware with other instances in same account. Use of physical server, automatic instance placement. per instance billing

## Spot Instance cancellation

1. To cancel a spot instance it important to cancel the spot request first.

2. Spot Feet = set of spot instances + (optional ) On Demand Instances

Spot Fleet allows us to automatically request Spot instance with the lowest price.

### Elastic Ip address

The instance public IP address changes when you stop and restart or terminate. So if we have an elastic Ip address and attach it to an instance, we can use the same IP address as the public ip address even when the instance starts again.

### Placement Group

1. Placement groups cluster
   EC2 spread across the same rack
2. Placement groups spread
   Ec2 in different availability zones
3. Placement group partition
   EC2 in same rack in different availability zones.

### Elastic Network Interface

it is a private Ip address it does not change and we can assign it to other instances.

### EC2 Hibernate

The in memory state RAM is preserved
The instance boot much faster
Ram state is written to a file in the root EBS volume
The root EBS volume must be encrypted

### EBS Volumes

EBS volumes are like network hard drives attached to an EC2 instance. We can detach and attach and EBS volume to another instance in the same availability sone.

We can take snap shots of EBS drives, default storage of snap short is standard we can also archive it to reduce cost but will be available back only with 24 oto 72 hours, we can also put it in a recycle bit if deleted accidentally.

### EC2 instance store

Ebs volume are network drives wit good but limited performance.
EC2 instance store is a high performance drive.

### EBS Volume Types

1. gp2/gp3 (ssd): General purpose SSD volume balances price and performance. 1GB to 16 TiB
2. Io/i02 (ssd): Provisioned IOPS Highest performance ssd volume for mission-critical low latency or high throughput workloads.More than 16000 IOPS
3. stl (HDD) Low cost HDD volume designed for frequency accessed workloads
4. scl (HDD) : lowest HDD volume designed for less frequently accessed workloads

### Amazon EFS - Elastic File system

1. Mananged NFS file system, works with EC2 instance in multi availability zones
2. Higher cost compated to `ebs `

### Load Balancer

1. Application Load balancer
2. Network Load balancer
3. Gateway load balancer

#### Application Load Balancer

Choose an Application Load Balancer when you need a flexible feature set for your applications with HTTP and HTTPS traffic. Operating at the request level, Application Load Balancers provide advanced routing and visibility features targeted at application architectures, including microservices and container.

#### Network Load Balancer

Choose a Network Load Balancer when you need ultra-high performance, TLS offloading at scale, centralized certificate deployment, support for UDP, and static IP addresses for your applications. Operating at the connection level, Network Load Balancers are capable of handling millions of requests per second securely while maintaining ultra-low latencies.

#### Gateway LoadBalancer

When you need to monitor traffic coming to your application. You can use a 3rd party virtual appliances can look into the traffic. Route tables are modified.

When you create an application loadbalancer you need to create a target group and forward the traffic to the target group,The target group must have the security group of the loadbalancer in it.

### Sticky Sessions - Cookie Names

To make the load balancer redirect the traffic from the user to the same instance behind the load balancer. This is done by using a cookie. The cookie has an expiration date.
Two types of cookies

1. Application-based cookies
2. Duration-based Cookies

### Enable cookies

DO to target grouo

Select the target group / Action / edit target group atrriutes

## Cross -Zone Load Balancing

Balance the load uniformly accross all instances

1. Application Load Balancer
   Cross zone Load balancing is enabled as default,
   No charges for inter Availability zone transfer

2. Network loadbalancer
   Disabled default
   Charges for inter availability zone transfer

## SSL Certificates

1. An ssl certificate allows traffic between your clients and your load balancer to be encrypted in transit. SSl refers to Secure Socket Layer used to encrypt connections.

2. TLS refers to a Transport Layer Security, which is a newer version.

3. Public SSSl certificates are used by Certificate Authorities(CA).

The load balancer an X.509 certificate (SSL/TLS cserver certificate)

## SSL - Server Name Indication (SNI)

SNI solves problem of loading multiple ssl certificates onto one web server ( to server multiple websites).
