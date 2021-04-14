

YCSB with Ansible
====================================
These YCSB play-books are operated only with mongoDB.

Getting Started
---------------
1. Download the ycsb.
     ```sh
     curl -O --location https://github.com/brianfrankcooper/YCSB/releases/download/0.17.0/ycsb-0.17.0.tar.gz
     tar -xzvf ycsb-0.17.0.tar.gz
     ```

2. Edit hosts file. You can use your own group names and host names.
    ```sh
    [server_ycsb]
    server1 ansible_host=127.0.0.1 
    server2 ansible_host=127.0.0.1 

    [server_ycsb:vars]
    remote_dir= "~/ycsb"
    ```
3. Add configuration files in config directory. You can make your own multiples config files.
    ```yaml
    ---
    # workload: a(default), b, c, d, e, f
    # insertorder: hashed(default), ordered
    # operationalcount: number of operations. default is 1000
    # recordcount: number of records to load.  default is 1000
    # maxexecutiontime: maximum execution time in seconds.  default is 60
    # readallfields: read all fields (true, default) or just one (false)
    # threads: number of client threads.  default is 1
    # engine: mongodb-async / mongodb(default)

    workload: a
    insertorder: ordered
    operationalcount: 5000000
    recordcount: 5000000
    maxexecutiontime: 300
    readallfields: true
    threads: 50
    ioengine: mongodb-async
    url: "mongodb://user:pass@165.1.1.1:27017/admin"
    ```
4. Run play books.

    Install:
    ```sh
    	ansible-playbook ycsb_install.yml -i hosts -k -e "INPUT_HOST=[your own group or host]"
    ```

    Run:
    ```sh
    	ansible-playbook ycsb_run.yml -e "INPUT_HOST=[group or host name], CONFIG_FILE=[config file name]"

    ```
5. Check results and logs.

    The hosts run the ycsb benchmark and save the logs in local file. playbook can fetch results to ansible master node. see the result directory in your ansible node.
