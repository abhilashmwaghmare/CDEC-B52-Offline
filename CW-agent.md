## Install CloudWatch Agent
 apt install amazon-cloudwatch-agent -y

 ## Create CloudWatch Agent Config

 vim /opt/aws/amazon-cloudwatch-agent/bin/config.json

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

## Start CloudWatch Agent

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
-a fetch-config \
-m ec2 \
-c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json \
-s


## to Verify the service  stopped/running

sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status

## Verify in AWS Console
