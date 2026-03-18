## step 1
sudo apt install -y curl unzip  
## step 2
curl -O https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
## step 3
sudo dpkg -i -E ./amazon-cloudwatch-agent.deb
## step 4
vim cwagent-config.json

{
  "metrics": {
    "namespace": "Custom/EC2",
    "metrics_collected": {
      "mem": {
        "measurement": [
          "mem_used_percent"
        ],
        "metrics_collection_interval": 60
      }
    }
  },
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/var/log/nginx/access.log",
            "log_group_name": "nginx-access-log",
            "log_stream_name": "{instance_id}"
          },
          {
            "file_path": "/var/log/nginx/error.log",
            "log_group_name": "nginx-error-log",
            "log_stream_name": "{instance_id}"
          }
        ]
      }
    }
  }
}


## Attach IAM Role

EC2 → IAM Role → Attach policy:

CloudWatchAgentServerPolicy
admin access
