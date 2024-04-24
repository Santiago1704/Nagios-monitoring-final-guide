Nagios Monitoring Guide 
=================

Authors (Autores) 
=================

| Author                | Origin                               |
| --------------------- | ------------------------------------ |
| Santiago Altamar      | UniBarranquilla - IUB                |
| Jenifer Barraza       | UniBarranquilla - IUB                |

Abstract
=================

Nagios is a powerful tool for monitoring IT infrastructure, ensuring the health and performance of networks, servers, applications, and services. This comprehensive guide offers step-by-step instructions for downloading and installing Nagios, enabling users to set up robust monitoring systems tailored to their specific needs. Whether you're a seasoned IT professional or a novice exploring monitoring solutions, this guide provides valuable insights and practical tips to maximize the efficiency and effectiveness of your monitoring efforts. From initial setup to advanced configurations, this guide equips you with the knowledge and tools necessary to harness the full potential of Nagios for proactive monitoring and maintenance of your IT environment. Get started today and empower your organization with real-time insights and proactive monitoring capabilities.

Screenshots
=================

Place text here

TOOLS TIC'S
=================

* Oracle Virtual Box
* Ubuntu Server
* Putty

Status
=================

| Status            | Description                          |
| ----------------- | ------------------------------------ |
| <img src="https://img.shields.io/badge/Study%20Status-Design%20Finalized-brightgreen.svg" alt="Study Status: Design Finalized"> | The study was finished | 

### Keyworks

- `Server`
- `Nagios`
- `Ubuntu`
- `Monitoring`
- `Plugin`
- `Cloud`

Roadmap
=================

	Pre-Requisites
	* Operating System: Choose a suitable operating system for Nagios installation. Nagios is compatible with various Linux distributions such as Ubuntu, Debian, CentOS, and Fedora. Select the distribution 	that you're most comfortable with and ensure it meets Nagios' system requirements.
	* Hardware Resources: Ensure that the host machine where Nagios will be installed has sufficient hardware resources. This includes CPU cores, RAM, and disk space. Nagios can consume significant 		resources, especially when monitoring a large number of hosts and services.
	* Network Configuration: Configure network settings for the Nagios host machine to ensure connectivity to other devices on the network. Set up networking according to your network requirements, ensuring 	that Nagios can communicate with the systems it monitors.
	* Access to Package Repositories: Ensure that the Nagios host machine has access to package repositories to install necessary software packages and dependencies. This may require configuring network 		settings or updating repository URLs if you're using a custom repository.
	* Basic Linux Skills: Familiarize yourself with basic Linux commands and system administration tasks. This includes navigating the file system, installing packages, editing configuration files, and 		managing services. Proficiency in Linux will streamline the installation and configuration process of Nagios.

	 Installation
  	* Linux Ubuntu 20.04
  	* Apache
 	* Plugins

		Server
			Item1
			Item2
			Item3 - plugins 
		Clientes (Client)


Steps for Nagios installation
=================
### Step 1: Upgrade the system and update the system packages to their latest versions
	sudo apt update
 	sudo apt upgrade

### Step 2: Install prerequisite packages
	sudo apt install wget unzip vim curl gcc openssl build-essential libgd-dev libssl-dev libapache2-mod-php php-gd php apache2

### Step 3: Download Nagios Core on Ubuntu 20.04
	export VER="4.4.6"
 	curl -SL https://github.com/NagiosEnterprises/nagioscore/releases/download/nagios-$VER/nagios-$VER.tar.gz | tar -xzf -
  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/f5b60c7d-b502-4a2b-8839-c09f8ecefcc4)

 
Next, let's download the Nagios kernel. You can check the versions page for the latest version. At the time of writing, the latest version of Nagios is v4.4.6.

### Step 4: How to install Nagios on Ubuntu
	cd nagios-4.4.6
 	./configure
  This will take a few seconds and be sure to get an example output shown below towards the end.
  
  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/5ddacaf0-ad84-468c-a36b-d9fee2335cda)

  To compile the main program along with the CGIs, run the make all command as follows.
  
	sudo make all
 
 Next, create the group users as follows.
 
 	sudo make install-groups-users
  	sudo usermod -a -G nagios www-data
   
   ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/f88d8003-8acc-449a-a488-48601f2273aa)

Next, install Nagios Core 4.x on your Ubuntu 20.04 system.

	sudo make install

 ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/18791ff4-9310-4b20-8a63-16282da7b13a)

 Towards the end, some additional instructions will be printed as shown above. Therefore, run the following command to install the init script in the path /lib/systemd/system.

 	sudo make install-init

  Next, install and set permissions on the directory containing the external command file.

  	sudo make install-commandmode

   Next, install the sample configuration files in /usr/local/nagios/etc/

   	sudo make install-config

At this point, activate the Apache module required for the Nagios web interface.

	sudo make install-webconf
	sudo a2enmod rewrite cgi
 	sudo systemctl restart apache2

  Also, feel free to install the Nagios exfoliation theme as follows:

  	sudo make install-exfoliation

   For the classic Nagios theme, run the following command.

   	sudo make install-classicui

    

   


### Usage (Por qué es importante usarlo)

Place text here

### FAQ (Preguntas y respuestas)

5 preguntas y respuestas

### Contacts (Contactos)

Place text here

### Acknowledgements (Agradecimientos)


