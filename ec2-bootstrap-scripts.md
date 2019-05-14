# Bootstrap scripts

- Scripts that are run when EC2 instances are _launched_ 
- Entered under _configure instance_ > _user data_
- Shell script, starts with shebang `#!/bin/bash`

## Example, installing apache on Amazon Linux

```bash
#!/bin/bash
yum update -y
yum install httpd -y
service httpd start
chkconfig httpd on
echo '<html><h1>Hello cloud</h1></html>' > /var/www/html/index.html
# Create bucket and upload the index to the bucket
aws s3 mb s3://mybucket
aws s3 cp /var/www/html/index.html s3://mybucket
```
