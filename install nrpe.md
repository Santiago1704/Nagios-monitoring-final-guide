How Install NRPE for Nagios
=================

Steps for Nagios installation
=================
### Step 1: download the necessary plugins 
	wget https://github.com/NagiosEnterprises/nrpe/releases/download/nrpe-4.1.0/nrpe-4.1.0.tar.gz
 
![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/f848075c-6a3a-4531-8604-580562ec8285)


### Step 2: Unpack  the downloaded files
	Tar -xzvf nrpe-4.1.0  


### Step 3:Configure Nrpe
    cd nrpe<tab to autocomplete>
	  ./configure
  

### Step 4:
Once the installation is done, execute the following command. This command is the executable used to query the server and will be useful for plugins:

	make check_nrpe
 	
  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/21dc4d0d-e92a-4d1b-9a28-2308560b34b2)

After completing the installation, execute the following command to install the plugins:
 
 	Make install_ plugin
   
  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/d5be597e-6ae4-4834-baea-7d6c747ad4ba)


Next, install Nagios Core 4.x on your Ubuntu 20.04 system.

	sudo make install

 ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/18791ff4-9310-4b20-8a63-16282da7b13a)

 ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/9ec2c3d8-5f4e-4c28-9f73-512608d73fb0)



 ### Step 5: 

We’ll create a command that allows Nagios to use the NRPE command we just set up. Navigate to the following location:

 	cd /usr/local/nagios/etc/objects/

Next, open the commands.cfg file using the vim editor or nano:

    vim commands.cfg
    nano commands.cfg

Scroll to the end of the file and add the following command definition:

    define command{
      command_name check_nrpe
      command_line $USER1$/check_nrpe -H $HOSTADDRESS$ -c $ARG1$
    }
  

### Step 6: Check instalation

    /usr/local/nagios/libexec/check_nrpe -H <IP_del_servidor_NRPE> -c <nombre_del_comando>

  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/36789283-ff33-430b-a67f-1c29a082022b)




Usage
=================

Installing NRPE (Nagios Remote Plugin Executor) is crucial for expanding the monitoring capabilities of Nagios. NRPE allows Nagios to remotely execute plugins on Linux/Unix machines and retrieve their results. This enables monitoring of local resources, services, and performance metrics that are not accessible directly from the Nagios server. By deploying NRPE, administrators can monitor critical aspects of their infrastructure, such as CPU usage, memory utilization, disk space, and specific application metrics, with greater granularity and accuracy. NRPE facilitates proactive monitoring and timely detection of issues, leading to faster troubleshooting and resolution. Additionally, NRPE enhances security by restricting access to sensitive system resources and ensuring that monitoring tasks are executed with appropriate permissions. Overall, integrating NRPE into the Nagios monitoring environment enhances its effectiveness and provides deeper insights into the health and performance of the entire infrastructure.

### Contacts

* saltamara@itsa.edu.co
* Jbarrazam@itsa.edu.co

### Acknowledgements 
* Tutorial: Nagios - Instalar NRPE (youtube.com)
* Nagios. Website: [Nagios Documentation](https://www.nagios.org/documentation/)
* Linux Academy: https://www.youtube.com/channel/UClGShptNEuvTWGAAfpa2Etw

