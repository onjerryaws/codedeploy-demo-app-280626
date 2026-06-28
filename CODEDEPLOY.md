# Installing the CodeDeploy agent on EC2
```
sudo yum update -y
sudo yum install -y ruby wget
wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
sudo service codedeploy-agent status
```

# create a bucket and enable versioning
```
aws s3 mb s3://hypha-codedeploy-20260409 --region us-east-1
aws s3api put-bucket-versioning --bucket hypha-codedeploy-20260409 --versioning-configuration Status=Enabled --region us-east-1
```

# deploy the files into S3
```
aws deploy push --application-name Hypha-DemoApp090426 --s3-location s3://hypha-codedeploy-20260409/codedeploy-demo/app.zip --ignore-hidden-files --region us-east-1
```

Buildspec.yml
```
artifacts:
  files:
    - '**/*'
```
