# amifinder
Python-based AMI finder

## Usage
```
Usage: amifinder [OPTIONS] INSTANCE_SIZE

Options:
  --os [amazon_minimal|ubuntu]  OS to search for
  --release TEXT                release of OS to search for
  --version TEXT                AMI version to search for
  --region TEXT                 region to query
  --help                        Show this message and exit.
```

## Examples
```bash
# Return the lastest AMI in the default region (us-west-2) for the default OS (amazon linux - minimal) for a t2.medium
$ amifinder t2.medium
ami-8076b2e0

# Return the latest AMI in the default region (us-west-2) for the default release of Ubuntu (16.04) for a t2.medium
$ amifinder t2.medium --os ubuntu
ami-746aba14

# Return the latest AMI in the default region (us-west-2) for the 14.04 release of Ubuntu for a t2.medium
$ amifinder t2.medium --os ubuntu --release 14.04
ami-70b67d10

# Return the latest AMI in us-east-1 region for the 14.04 release of Ubuntu for a t2.medium
$ amifinder t2.medium --os ubuntu --release 14.04 --region us-east-1
ami-8e0b9499

# Return the AMI in the us-east-1 region for the 20160509.1 version of the 14.04 release of Ubuntu for a t2.medium
$ amifinder t2.medium --os ubuntu --release 14.04 --region us-east-1 --version 20160509.1
ami-7c927e11
```

## Notes
* All instances assume a EBS root volume 
