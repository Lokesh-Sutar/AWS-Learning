# Network File System (NFS)
- It is a distributed file system protocol.
- Allows users to access files over a network.
- Default port is 2049.
- Elastic File System (EFS) primarily uses the NFS protocol

## Steps to connect EFS to EC2 Instance using NFS
1. Launch EC2 instance.

2. Create IAM Role with `AmazonElasticFileSystemFullAccess` permission.

3. Attach role to EC2 instance  using following steps:
    - Right Click on Instance
    - Security
    - Modify IAM Role

4. Create an EFS File System in the same region with default settings

5. Create `Security Group` (EC2->Security Group) with Inbound Rule of `NFS` and Outbound Rule of NFS (Only if All traffic is not set by default)

6. Attach this Security Group (SG) to EFS with following steps:
    - EFS
    - Network
    - Manage
    - Select this SG to all zones

7. Now Configure the EC2 Instance with following steps:
    - Instance
    - Security
    - Security Groups
    - Inbound Rules
    - Edit Inbound Rules
    - Add Rule
    - Select NFS with 0.0.0.0/0
    - Default Outbound Rule is All traffic (so no changes here)
        - If not then Select NFS with 0.0.0.0/0

8. Install NFS Client on EC2 Instances
   - SSH into each EC2 instance.
   - Install the NFS client using the following commands:
        ```
        sudo yum -y update
        sudo yum -y install nfs-utils
        ```

9. Mount the EFS File System
   - Create a directory to mount the EFS:
        ```
        sudo mkdir /mnt/efs
        ```

   - Mount the EFS file system:
        ```
        sudo mount -t nfs4 -o nfsvers=4.1 <EFS_DNS_Name>:/ /mnt/efs
        ``` 
   - Verify the mount:
        ```
        df -h
        ```

10. Test the File System
   - Create a test file:
        ```
        echo "Hello EFS" | sudo tee /mnt/efs/hello.txt
        ```
   - Verify the file is accessible from another EC2 instances:
        ```
        cat /mnt/efs/hello.txt
        ```  

Cleanup
- Unmount the EFS file system:
    ```
    sudo umount /mnt/efs
    ```

- Terminate the EC2 instances.
- Delete the EFS file system from the console.