# Vault Dynamic AWS Demo

## This is a simple demo to dynamically create AWS credentials using Vault, renew them, and revoke them.  The `lease` and `lease_max` values are set to `1m` to quickly show how AWS access can be ephemeral.  You can modify these values in the `1_aws_dynamic_creds.sh` script to accommodate your demo.

## Requirements: 
#### A. HashiCorp's Vault binary installed on your machine and having the `PATH` configured.
#### B. You will need both `AWS_ACCeSS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` set in your environment variables.  This is what Vault will use to interact with AWS.

#### 1.  Open a terminal window and run the first script `0_start_vault.sh` to start your Vault server in `dev` mode.  It will generate the root token as `root` so you can easily login.

#### 2.  Open another terminal window and run the second script `1_aws_dynamic_creds.sh` will will configure Vault with the AWS secret engine with a `policy_document` that allows any action against the EC2 server.

#### 3.  (Optional) Run the third script `2_renew_creds.sh` in case you need additional time for your AWS demo.

#### 4.  Once your demo is complete, or to show revocation, copy the `lease_id` that was generated from the `1_aws_dynamic_creds.sh` script.  It should look something like `aws/creds/my-role/0bce0782-32aa-25ec-f61d-c026ff22106e` but you only need to copy the `0bce0782-32aa-25ec-f61d-c026ff22106e` value to your clipboard.  Then, run the last script `3_revoke_creds.sh` which will insert the value you copied from your clipboard and revoke those AWS credentials.

#### You can now return to your terminal running the Vault server process and kill it using `Ctrl-C`
#### WARNING: If you kill your Vault server before Vault revokes the AWS creds you generated earlier, the AWS creds will continue to persist.  Vault needs to be online so you can revoke it manually or allow the TTL to expire.
