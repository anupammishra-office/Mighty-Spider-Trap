# Mighty-Spider-Trap



Collection of \[SSM

Documents](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-ssm-docs.html).



These documents let you perform chaos engineering experiments on

resources (applications, network, and infrastructure) in the \[AWS

Cloud](https://aws.amazon.com).



SSM Automation documents:

=========================



To use SSM Automation, check \[the

link](https://medium.com/@adhorn/creating-your-own-chaos-monkey-with-aws-systems-manager-automation-6ad2b06acf20)



\-   Support for (randomly) stopping EC2 instances via API

\-   Support for (randomly) stopping EC2 instances via AWS Lambda

\-   Support for (randomly) terminating EC2 instances via API

\-   Support for detaching EBS volumes from EC2 instances via API

&nbsp;   (ec2, ebs)

\-   Support for rebooting RDS instance with proper tags via API

\-   Support for CPU stress scenario via Run Command



Upload an SSM Automation document:

==================================



``` {.sourceCode .shell}

aws ssm create-document --name "StopRandomInstances-API" --content file://stop-random-instance-api.yml --document-type "Automation" --document-format YAML

```

Upload all of the SSM Documents to the AWS region of your choice

================================================================



``` {.sourceCode .shell}

cd chaos-ssm-documents/run-command



./upload-document.sh -r eu-west-1 (or other region of your choice)

```





\*\*Support Canceling \& Rollback (10s max)\*\*





\-   Support for killing a process by name using `kill-process.yml`

\-   Support for CPU stress using `cpu-stress.yml`

\-   Support for IO stress using `io-stress.yml`

\-   Support for memory stress using `memory-stress.yml`

\-   Support for diskspace stress using `diskspace-stress.yml`

\-   Support for latency injection to network traffic on a particular network interface using `latency-stress.yml`

\-   Support for latency injection with jitter to outgoing or incoming traffic from a configurable list of sources (Supported: IPv4, IPv4/CIDR, Domain name, DYNAMODB|S3) using `latency-stress-sources.yml`

\-   Support for packet loss injection to network traffic on a particular network interface using `network-loss-stress.yml`

\-   Support for packet loss injection to outgoing or incoming traffic from a configurable list of sources (Supported: IPv4, IPv4/CIDR, Domain name, DYNAMODB|S3) using `network-loss-sources.yml`





\*\*Experimental\*\*



\-   Support for blackhole S3 stress using `blackhole-s3-stress.yml`

\-   Support for blackhole DynamoDB stress using `blackhole-dynamo-stress.yml`

\-   Support for blackhole EC2 stress using `blackhole-ec2-stress.yml`





\*\*Prerequisites\*\*



\-   \[SSM

&nbsp;   Agent](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-install-ssm-agent.html)

&nbsp;   (Preinstalled on several Amazon Machine Images)

\-   \[stress-ng, tc, and

&nbsp;   jq](https://github.com/adhorn/chaos-ssm-documents/blob/master/run-command/install-dependencies.yml)

&nbsp;   (Automatic install of dependencies)



Upload one document at a time

=============================



``` {.sourceCode .shell}

cd chaos-ssm-documents/automation



aws ssm create-document --content file://cpu-stress.yml --name "cpu-stress" --document-type "Command" --document-format YAML

```



Upload all of the SSM Documents to the AWS region of your choice

================================================================



``` {.sourceCode .shell}

cd chaos-ssm-documents/run-command



./upload-document.sh -r eu-west-1 (or other region of your choice)

```



