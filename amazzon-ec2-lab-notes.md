# EC2 Lab — Senior Engineering Notes

These notes reflect practical considerations, efficiency tips, and pitfalls from working with EC2 instances, written from a senior cloud engineer perspective.

## Launching EC2 Instances
- Use region-specific AMIs; check `ami-xxxxxxx` before running.
- Pick instance type based on workload; `t2.micro` is only for testing.
- Tag resources consistently for easier management.
- Avoid leaving instances running; automate cleanup.
- Watch out for `InvalidAMIID.NotFound` or `InsufficientInstanceCapacity`.

## SSH Access & Key Management
- Private key must be `chmod 400`.
- Username varies by OS (`ec2-user` vs `ubuntu`).
- Common errors: `Permission denied (publickey)`, `Connection timed out`.
- Use EC2 Instance Connect when possible.
- Restrict SSH access in security groups; don’t open port 22 to everyone.

## Metadata & Instance Inspection
- Metadata URL: `http://169.254.169.254/latest/meta-data/`
- Useful for scripts and dynamic configuration.
- Avoid exposing metadata to public applications.
- Don’t hardcode instance IDs; use tags or metadata.

## Termination & Cleanup
- Always terminate instances to prevent unnecessary cost.
- Remove EBS volumes and snapshots if not needed.
- Use `aws ec2 wait instance-terminated` in scripts.
- Automate cleanup for multiple instances using tags or Lambda.

## General Tips
- Automate repeatable workflows with scripts or IaC.
- Use Git for version control of scripts and notes.
- Monitor costs even for lab environments.
- Document reasoning behind choices (instance type, AMI, key, security).
- Capture logs for troubleshooting (`stderr` and `stdout`).
