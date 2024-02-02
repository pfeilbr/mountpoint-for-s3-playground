# mountpoint-for-s3-playground

learn [Mountpoint for Amazon S3](https://github.com/awslabs/mountpoint-s3)

- support of posix file system apis: create, read, and delete files.  does not support updates to existing files.

## demo

```sh
# install Mountpoint for Amazon S3 client

# for amzn linux, centos, redhat
wget https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.rpm
sudo yum install -y ./mount-s3.rpm

# or for debian

wget https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.deb
sudo apt-get install -y ./mount-s3.deb

# set credentials for `mount-s3` client to use
export $(printf "AWS_ACCESS_KEY_ID=%s AWS_SECRET_ACCESS_KEY=%s AWS_SESSION_TOKEN=%s" \
$(aws --profile "PROFILE_NAME" sts assume-role \
--role-arn arn:aws:iam::xxxxxxxxxx:role/s3-full-access \
--role-session-name MySessionName \
--query "Credentials.[AccessKeyId,SecretAccessKey,SessionToken]" \
--output text))

# show all options
mount-s3 --help

# mount with no delete
mount-s3 <bucket name>  ~/mnt/s3

# mount with delete
mount-s3 --allow-delete "com.brianpfeil.scratch01" ~/mnt/s3

# unmount
sudo umount ~/mnt/s3

# `--allow-delete` - the corresponding object is immediately deleted from your S3 bucket.
# `--read-only` - forbid all mutating actions on your S3 bucket

```

## resources

- <https://github.com/awslabs/mountpoint-s3>
- [Configuring Mountpoint for Amazon S3](https://github.com/awslabs/mountpoint-s3/blob/main/doc/CONFIGURATION.md)