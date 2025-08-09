![[Pasted image 20221030221245.png]]
# AMI (Amazone Machine Image)

## TLDR

AMIs are **preconfigured** [[EC2]] Instance templates. AMIs allow further customisation of your instances, right on startup of an instance. You can create your own custom AMI or choose one AWS and other users have already build (AWS Marketplace).

**Types**:

- **Public AMI**: Provided by AWS.
- **Custom AMI**: Your own AMI, created from a running instance. Locked to a region, can be manually copied to another region.
- **An AWS Marketplace AMI**: 3rd party AMIs, might cost money.

## How to create your own AMI

- Start [[EC2]] instance.
- Run scripts/setup and add all data you want the AMI to have.
- Stop [[EC2]] instance.
- Build AMI (also creates an [[EBS]] Snapshot, if you delete this snapshot the AMI wont work).
- Launch new instances with your freshly created AMI.

---

**Golden AMI**: pre-configured AMI used as a reference for creating other AMIs. Quickly and consistently create new instances configured with the same software and settings.
