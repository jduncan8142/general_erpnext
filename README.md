# ERP Next General Notes & Code
General notes and code for ER Next deployments
## Install Instructions for ERP Next 13 on Ubuntu 20.04 as of 2021.05.17

0. As root run the following:
    ```
    sudo su
    ```

1. Step-1
    ```
    apt-get update -y && apt-get upgrade -y
    ```

2. Step-2
    ```
    curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
    ```

3. Step-3
    ```
    apt install -y nodejs mariadb-server redis-server python3-pip nginx python3-testresources
    ```

4. Step-4
    ```
    adduser frappe
    ```
    ```
    usermod  -aG sudo frappe
    ```

 5. Step-5
    1. Edit:
        ```
        nano /etc/mysql/my.cnf
        ```
    2. Add the following lines:
        ```
        [mysqld]
        character-set-client-handshake = FALSE 
        character-set-server = utf8mb4 
        collation-server = utf8mb4_unicode_ci 

        [mysql]
        default-character-set = utf8mb4
        ```

6. Step-6
    ```
    systemctl restart mysql
    ```

7. Step-7
    ```
    mysql_secure_installation
    ```

8. Step-8
    ```
    #Enter current password for root (enter for none): Press your  [Enter] key, there is no password set by default
    #Set root password? [Y/n] Y
    #New password:
    #Re-enter new password:
    #Remove anonymous users? [Y/n] Y
    #Disallow root login remotely? [Y/n] N
    #Remove test database and access to it? [Y/n] Y
    #Reload privilege tables now? [Y/n] Y
    ```

9. Step-9
    ```
    mysql -u root -p
    ```

10. Step-10
    ```
    MariaDB [(none)]USE mysql;
    ```
    ```
    MariaDB [(none)]UPDATE user SET plugin='mysql_native_password' WHERE User='root';
    ```

11. Step-11
    ```
    MariaDB [(none)] FLUSH PRIVILEGES;
    ```
    ```
    MariaDB [(none)] EXIT;
    ```

12. Step-12
    ```
    sudo npm install -g yarn
    ```
    ```
    node -v && npm -v && python3 -V && pip3 -V && yarn -v
    ``` 

13. Step-13 
    ```
    pip3 install frappe-bench
    ```

14. Step-14
    ```
    systemctl restart mariadb
    ```

15. Step-15
    ```
    su frappe
    cd
    sudo pip3 install frappe-bench
    ```

16. Step-16
    ```
    sudo -H pip3 install frappe-bench
    ```
    ```
    bench --version
    ```

17. Step-17
    ```
    bench init --frappe-branch version-13-beta frappe-bench
    ```

18. Step-18
    ```
    cd frappe-bench
    ```

19. Step-19
    ```
    bench new-site <yourdomain.com>
    ```

20. Step-20
    ```
    bench get-app --branch version-13-beta erpnext
    ```

21. Step-21
    ```
    bench new-site <yourdomain.com>
    ```

22. Step-22
    ```
    bench --site <yourdomain.com> install-app erpnext
    ```
