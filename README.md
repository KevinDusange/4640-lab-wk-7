# 4640-lab-wk-7

### completed by: kevin dusange, gautam dhoophar, philip flores

### pre-reqs
```bash
sudo apt install ansible
sudo apt install yamllint
```

## Step 1: Create a new SSH key pair

First we created the key pair using the command:
```bash
ssh-keygen -t ed25519 -f ~/.ssh/aws
```

Then we imported the newly created public to the AWS account using the "import_lab_key" script using the command:
```bash
./scripts/import_lab_key ~/.ssh/aws.pub
```

## Step 2: Running the terraform configuration

After the keys were craeted and imported we ran first ran `terraform init` in the terraform directory which then successfully initialized terraform. Then we ran `terraform fmt` to automatically format the config file, then `terraform validate` which was a success and showed us that the configuration is valid, followed by the `terraform plan` command which showed us a preview of the changes that terraform will make. Finally after everything was verified and good, we ran the `terraform apply` command which created the ec2 instances and provided the DNS names, and public IP addresses of the 2 instances after it finished applying the changes and finally we uploaded the DNS names into the hosts.yml file.

## Step 3: Completing the `playbook.yml` file

After creating the `playbook.yml` file, the issue it gave us when we ran the file was "no package matching nginx is available" so we needed to also update the package manager before installing nginx. After adding that in, it seemed to fix the issue. The command we ran to check the syntax of the file was:
```bash
ansible-playbook --syntax-check playbook.yml
```

Then to run the playbook file we ran the command:
```bash
ansible-playbook playbook.yml
```

After running the playbook and all the tasks were completed/successful, we visited the DNS name of the first server which verified that it was successful.

<img width="944" height="411" alt="Screenshot 2025-10-17 222715" src="https://github.com/user-attachments/assets/8fb3a388-45fc-4b16-a2ce-1b547e751165" />

Once we made sure the lab was finished we deleted the ssh key and removed the resources created by terraform using the 2 commands below:
```bash
terraform destroy
./delete_lab_key
```





