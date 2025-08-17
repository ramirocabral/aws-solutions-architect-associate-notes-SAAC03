![[kms.png]]

## Overview

- Create and manage cryptographic keys.
- Control use of keys.
- Integrated with IAM for auth.
- Can audit use of keys via CloudTrail.
- Billed per 10000 api calls.
- Scoped per region..
- Seamlessly integrated into most AWS services.

## Key Types

### Symetric

- AES256.
- Single key to encrypt and decrypt.
- AWS services which use KMS use this.
- You never get access to the KMS Key unencrypted. Must call KMS API to use it.

### Asymetric

- RSA and ECC.
- Public key (encrypt).
- Private key (decrypt).
- Can download Public Key.
- Private key only through KMS API.
- Use case: encryption outside of aws by users who can't call the KMS API.

## Types of KMS Keys

- **AWS Owned Keys** (free)
  - SSE-S3, SSE-SQS, SSE-DDB (default key).
  - An AWS service owns them and manages to use in multiple accounts.

- **AWS Managed Keys** (free)
  - Usually called (aws/service-name).
  - Created, managed and used on the customer's behalf by AWS.

- **Customer Managed keys** (1$ per month)
  - Can be created in KMS or imported.

- **CloudHSM Keys** (custom keystore)
  - Key generated from your own CloudHSM hardware device.

## Key Rotation

### AWS Managed Key

- Automatic every 1 year

### Customer-Managed KMS Key

- Must be enabled.
- Automatic and on-demand.
- If imported, only manual rotation possible using alias.

## Key Policies

- Control access to KMS keys.
- Similar to [[S3]] policies. Difference: you cannot control access without them.
- **Default** = Everyone in your account can use the key.
- **Custom KMS Key Policy** : Define users, roles that can access the key. Define who can administer the key. Used for cross account.

### Copying Snapshots Across Accounts

1. Create Snapshot, encrypted with your own KMS key (Customer Managed Key).
2. **Attach a KMS Key Policy** to authorize cross-account access.
3. Share the encrypted snapshot.
4. (in target) Create a copy of the Snapshot, encrypt it with a CMK in your account.
5. Create a volume from the Snapshot.

## Multi Region Keys

- Keys are replicated with same ID into different regions.
- Multi-Region keys have the same ID, key material, rotation policies.
- Encrypt and decrypt in other regions. No need to making cross-regions API calls.
- They **are NOT global**. (primary + replicas).
- Each Multi-Region key is managed **independently**.
- Use case to encrypt global services ([[Aurora]] global, [[DynamoDB]] global tables).

## Encrypt DDB Global Tables

- Can encrypt specific attirubtes client-side in our DDB Table using the **Amazon DynamoDB Encryption Client**.
- Using client-side encryption, we can protect specific fields and guarantee only decryption if the client has access to an API key.

![[kms_ddb.png]]

- Same concept for [[Aurora]] global DB.

## [[S3]] Replication

- **Unencrypted objects and objects encrypted with SSE-S3 are replicated by default.**
- Objects encrypted with SSE-C (customer provided keys) can be replicated.

- **For objects encrypted with SSE-KMS**, need to enable the option.
  - Specify which KMS key to encrypt the objects within the target bucket.
  - Adapt the key policy for the target key.
  - An IAM Role with kms:Decrypt for the source KMS Key and kms:Encrypt for the target KMS Key.
- **Can use multi-region KMS Keys, but they are currently treated as independent keys by S3**.

## AMI Sharing Process Encrypted via KMS

1. AMI in Source Account is encrypted with KMS Key from Source Account.
2. Must modify the image attribute to add a **Launch Permission** which corresponds to the specified target AWS account.
3. Share the KMS Key used to encrypt the snapshot the AMi references with the target account / IAM Role.
4. The IAM Role / User in the target account must have the permisisons to: DescribeKey, ReEncrypt, CreateGrant, Decrypt.
5. Launch an [[EC2]] instance from the AMI, optionally the target account can specify a new KMS key in its own account to re-encrypt the volumes.

![[kms_ami_sharing.png]]
