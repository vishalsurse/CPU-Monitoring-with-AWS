# CPU-Monitoring-with-AWS
AWS EC2 Instance and Monitoring CPU Utilization using Grafana

# Install Grafana on Amazon Linux

Step 1:  

Add Grafana Repository
sudo tee /etc/yum.repos.d/grafana.repo <<EOF
[grafana]

name=grafana

baseurl=https://packages.grafana.com/oss/rpm

repo_gpgcheck=1

enabled=1

gpgcheck=1

gpgkey=https://packages.grafana.com/gpg.key

sslverify=1

EOF

# Step 2: Install Grafana

sudo yum install grafana -y

Step 3: Start & Enable Grafana Service

sudo systemctl daemon-reload

sudo systemctl start grafana-server

sudo systemctl enable grafana-server

Step 4: Check Grafana Status

systemctl status grafana-server

# Access Grafana UI

Open browser

URL: http://<EC2-PUBLIC-IP>:3000

Default Login:

Username: admin

Password: admin

# Configure AWS CloudWatch in Grafana

Step 1: 

Create IAM Role

Go to IAM → Roles → Create Role

Trusted entity: AWS Service → EC2

Attach policy: CloudWatchReadOnlyAccess

Attach role to EC2 instance

Step 2: 

Add CloudWatch Data Source

Grafana → Settings → Data Sources

Add CloudWatch

Authentication: AWS SDK Default

Save & Test

# Create CPU Utilization Dashboard
 
Step 1: 

Create Dashboard

Grafana → + → Dashboard

Add new panel

Step 2: 

Configure Metrics

Data source: CloudWatch

Namespace: AWS/EC2

Metric: CPUUtilization

Dimension: InstanceId

Step 3: 

Visualization

Graph type: Time Series

Unit: Percent (%)

Save dashboard
