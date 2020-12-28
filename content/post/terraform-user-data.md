---
title: "Terraform initialization script with user_data"
date: "2020-12-23"
author: "Tristina"
---


If you want to install git or python once Terraform create your EC2 instance. Then [user_data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html) could be useful. 


### Run few command

If you only need to run two or three commands you can use this syntax.

```json  
resource "aws_instance" "ec2_instance" {
  count                       = "${var.instance_count}"
  ami                         = "${data.aws_ami.ec2_amzn2_ami_hvm.id}"
  instance_type               = "${var.instance_type}"
  subnet_id                   = "${var.subnet_id}"
  associate_public_ip_address = true
  monitoring                  = false
  key_name                    = "${var.key_name}"
  availability_zone           = "${var.availability_zone}"
  vpc_security_group_ids      = ["${aws_security_group.ec2_security_group.id}"]
  #User data field
  user_data                   = << EOF
		                        #! /bin/bash
                                sudo yum update -y
		                        sudo yum install -y git wget
  EOF
  
  tags = {
    Name = "user-data-instance-example"
  }
}
```

### Use a script file

If your script it's more complicated you may like to use a file.

```json 
resource "aws_instance" "ec2_instance" {
  count                       = "${var.instance_count}"
  ami                         = "${data.aws_ami.ec2_amzn2_ami_hvm.id}"
  instance_type               = "${var.instance_type}"
  subnet_id                   = "${var.subnet_id}"
  associate_public_ip_address = true
  monitoring                  = false
  key_name                    = "${var.key_name}"
  availability_zone           = "${var.availability_zone}"
  vpc_security_group_ids      = ["${aws_security_group.ec2_security_group.id}"]
  #User data field
  user_data                   = "${file("${path.module}/install.sh")}"
  
  tags = {
    Name = "user-data-instance-example"
  }
}
```


The user data field it's specific to AWS EC2, Terraform also provides [provisioner](https://www.terraform.io/docs/provisioners/index.html). You should compare and think about the [difference](https://stackoverflow.com/questions/44378064/terraform-should-i-use-user-data-or-provisioner-to-bootstrap-a-resource) between provisioner and user_data.

Example's available on [GitHub](https://github.com/smlc/terraform-user-data).
