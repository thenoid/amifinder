# amifinder
Python-based AMI finder

## Usage
```
Usage: amifinder [OPTIONS] INSTANCE_SIZE

Options:
  --owner TEXT    owner of this AMI.  defaults to "self"
  --os TEXT       OS to search for
  --version TEXT  AMI version to search for
  --release TEXT  Release of OS to search for
  --pattern TEXT  pattern to use for Name.  See README.md for details
  --region TEXT   region to query
  --help          Show this message and exit.
```

## Examples
```bash
# Return the lastest AMI in the default region (us-west-2) for the default OS (amazon linux) for a t2.medium
$ amifinder t2.medium
ami-7172b611

# Return the latest AMI in the default region (us-west-2) for the 16.04 release of Ubuntu for a t2.medium
$ amifinder --owner canonical --os ubuntu --release 16.04 t2.medium
ami-e1fe2281

# Return the latest AMI in the default region (us-west-2) for the 14.04 release of Ubuntu for a t2.medium
$ amifinder --owner canonical --os ubuntu --release 14.04 t2.medium
ami-a24598c2

# Return the AMI in the us-east-1 region for the 20160509.1 version of the 14.04 release of Ubuntu for a t2.medium
$ amifinder  --owner canonical --os ubuntu --release 14.04 --version 20160509.1 --region us-east-1 t2.medium
ami-7c927e11

# Return the latest AMI in the default region (us-west-2) for a self-published Ubuntu base AMI with a specified name pattern
$ amifinder --owner self --os ubuntu_base --pattern "OS.VERSION.RELEASE" t2.medium
ami-af36eacf
```

## The --pattern parameter
The `--pattern` parameter specifies a format for the name given to an AMI.  This is helpful when you have self-published
AMIs to specify the specific fields to look for in the name:
* `--os` - replaces `OS` in the pattern
* `--version` - replaces `VERSION` in the pattern
* `--release` - replaces `RELEASE` in the pattern

### Example
```
# Self published AMI with a name: amazon_base.20160922.01
# --pattern = OS.VERSION.RELEASE
# --os = amazon_base
# --version = 20160922
# --release = 01
$ amifinder --owner self --os amazon_base --version 20160922 --release 01 --pattern "OS.VERSION.RELEASE" t2.medium
ami-8f37ebef
```

## Notes
* All instances assume a EBS root volume 
