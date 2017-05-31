# n-vijaykarthik.devops.github.io
Learning and Sharing DevOps Related examples and scenarios
Based on my availability of my schedule i will be including scenarios, examples with respect to tools like Ansible, Chef, Puppet, SaltStack...

## List of Tools
- Ansible
- Chef
- Puppet
- SaltStack

# Puppet


The following command is used to check if puppet is installed on exisiting systems:
![alt tag](https://cloud.githubusercontent.com/assets/17361962/26610493/d27de76a-4575-11e7-8fde-701bf3db82fb.PNG)

Execute the following command for install puppet package
![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611122/0043f46a-457a-11e7-88e7-5d30bca3753b.PNG)

- Incase if any issues with subscription manager during puppet package install then execute the following command else skip to next command
  ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611258/0f17f2e2-457b-11e7-89bf-5db7cccd43b8.PNG)

Execute the following command for installing puppet server
![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611176/6ca33a30-457a-11e7-8810-35932860b8ed.PNG)

you will finally see some dependencies been processed and finally the following message confirms that puppet server is installed
![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611200/a7bdbd7a-457a-11e7-8500-dba4de551f82.PNG)

The following command shows the list of resources available on puppet
![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611311/7e286cf2-457b-11e7-94ad-796f5006f7fc.PNG)

- To install a specific module using puppet execute the following command
  for example "vim" is not installed in the exisiting..
  
  ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611355/d0ed6884-457b-11e7-810a-6b7ad64fe4a1.PNG)
  
   As of today there are 4k+ modules available on puppet forge.
   
   execute the following command to install "vim" online(using internet) from puppet forge which give a lot of options
   select any of the "vims" that is required as per the scenario.
   ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611383/f5308e60-457b-11e7-8f07-273ee76dc7d1.PNG)
   
   Following is to install dhoppe-vim from puppet forge.
   ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611457/6cec90c0-457c-11e7-9edd-bc11b1e39277.PNG)
   
   Once installation is done, check it using the following command
   ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611502/b8c0d164-457c-11e7-9ec4-92b32dd6f8a7.PNG)
   
   In case if any installed module requires uninstallation then following command can be used for uninstalling of unwanted modules
   Make sure to check the modulename that needs to uninstalled. example shows vim cannot be uninstalled but dhoppe-vim can be uninstalled.
   ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611518/d965c6ae-457c-11e7-9bb9-0c9c1915463f.PNG)
   
  -  The following is to install a puppet master and agent nodes if for Compex Infrastructure where more than one node needs continous automation.
  The puppet config file has two parts [agent] is generally the number of nodes or clients on which you need to install puppet and 
  [main] where actual master or server node details are given.
  ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611710/f0c7b59a-457d-11e7-8879-bcbca401f364.PNG)
  
  The following config shows adding master for DNS
  ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611771/6964a5ee-457e-11e7-9c84-94ca8c7f88e4.PNG)
  
  Both the server and client **IP Address** should be mentioned in /etc/hosts file in order to communciate with each other.
   
   Once completing the above step create ** SSL Certificate** on master for secure authentication purpose 
   ![alt tag](https://cloud.githubusercontent.com/assets/17361962/26611856/1304014e-457f-11e7-8c57-f7c917960392.PNG)
   
   Install "puppet rpm_module" on client to install puppet and then execute " puppet agent -t " 
   
   Execute "puppet ca --sign 'client.node.com' " on Puppet Master node or server to accept the ca certificate from client for establishing secure communication.


- The following is the manifest file that needs to be edited on Puppet Master node or server for every new client
  create a file named "site.pp" in /etc/puppet/manifests/
  //node default{
  node client1.xyz.com{
  file {'/etc/motd':
  content => 'My Testing Content',
  }

  service{'postfix':
  ensure=>'stopped'
  enable=>'false',
  }
  }
