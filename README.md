# amifinder
Python-based command line tool to find AMI IDs for a few OSes

PyPi project: [amifinder](https://pypi.python.org/pypi/amifinder/0.0.3)

## Usage
```
# AMI Finder Help
Usage: amifinder [OPTIONS] COMMAND [ARGS]...

Options:
  -V      Show the version and exit.
  --help  Show this message and exit.

Commands:
  find
  info
  
# AMI Finder Find
Usage: amifinder find [OPTIONS] INSTANCE_SIZE

Options:
  --owner TEXT    owner of this AMI.  defaults to "amazon"
  --os TEXT       OS to search for
  --version TEXT  AMI version to search for
  --release TEXT  Release of OS to search for
  --pattern TEXT  pattern to use for Name.  See README.md for details
  --region TEXT   region to query
  --verbose
  --help          Show this message and exit.

# AMI Finder Info
Usage: amifinder info [OPTIONS] AMI_ID

Options:
  --region TEXT  region to query
  --help         Show this message and exit.
```

## Examples
```bash
# Show the current version
$ amifinder -V
0.0.3

# Return the lastest AMI in the default region (us-west-2) for the default OS (amazon linux) for a t2.medium
$ amifinder find t2.medium
ami-7172b611

# Return the latest AMI in the default region (us-west-2) for the 16.04 release of Ubuntu for a t2.medium
$ amifinder find --owner canonical --os ubuntu --release 16.04 t2.medium
ami-167ba776

# Return the latest AMI in the default region (us-west-2) for the 14.04 release of Ubuntu for a t2.medium
$ amifinder find --owner canonical --os ubuntu --release 14.04 t2.medium
ami-a24598c2

# Return the AMI in the us-east-1 region for the 20160509.1 version of the 14.04 release of Ubuntu for a t2.medium
$ amifinder find --owner canonical --os ubuntu --release 14.04 --version 20160509.1 --region us-east-1 t2.medium
ami-7c927e11

# Return the latest AMI in the default region (us-west-2) for a self-published Ubuntu base AMI with a specified name pattern
$ amifinder find --owner self --os ubuntu_base --pattern "OS.VERSION.RELEASE" t2.medium
ami-af36eacf

# Show the details about AMI ami-af36eacf
$ amifinder info ami-af36eacf | jq '.'
{
  "state": "available",
  "ami_id": "ami-af36eacf",
  "name": "ubuntu_base.20160922.01",
  ...
  "virtualization_type": "hvm",
}
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
