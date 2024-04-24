Nagios Monitoring Guide 
=================

Authors
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

![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/1334a66c-3b9c-44b1-bdf9-b7ae607d26b7)

![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/45e7dd20-03c2-4a8f-9d2a-13f6d761ca7d)



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

 ### Step 5: Create a Nagios web login user

 	sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin

  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/fd831adf-3247-46be-8297-4606039e2d6c)

  The password is written in the /usr/local/nagios/etc/htpasswd.users file.
  

### Step 6: Install Nagios plugins
To download the plugins, run the command

	VER="2.3.3"
 	curl -SL https://github.com/nagios-plugins/nagios-plugins/releases/download/release-$VER/nagios-plugins-$VER.tar.gz | tar -xzf -

  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/97145cbc-3640-43ce-ba72-8a849c92e708)

  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/688ce2f3-6ed0-4fa8-b552-f0c1ab6cf4fe)

To install the plugins, navigate to the source directory of the plugins:

	cd nagios-plugins-2.3.3

 A continuación, compila los plugins de Nagios desde el código fuente de la siguiente manera:

 	./configure --with-nagios-user=nagios --with-nagios-group=nagios
  	sudo make install

   Una vez terminada la instalación verifica que todas las configuraciones estén en orden como se muestra.

   	sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

   ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/372f1027-cbcd-443b-a66e-caf747145953)

   
### Step 7: Start and enable the Nagios daemon

To start the Nagios service run:

	sudo systemctl enable --now nagios

 Confirm that the Nagios service is running.

 	sudo systemctl status nagios

  ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/79848748-930c-4aff-a033-2cf1c053cce2)

### Step 8: Log in to Nagios

And finally, we come to the last step where we will access Nagios. To do this, simply open your web browser and go to the URL shown.

	http://ip_servidor/nagios

 You will be prompted to authenticate in the pop-up window that is displayed. Use the credentials you provided in step 5 and click the “Login” button.

 ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/cbb1ac4e-61c5-4fa6-8816-da1fe14ab8c6)

 ![image](https://github.com/Santiago1704/Nagios-monitoring-final-guide/assets/84638545/415f9746-cdcb-4d74-a51f-fa6520507c10)




Usage
=================

Nagios plays a pivotal role in modern IT operations by providing comprehensive monitoring capabilities for infrastructure, applications, and services. Nagios enables proactive monitoring, allowing administrators to identify and address potential issues before they impact system performance or availability. With customizable dashboards, alerts, and reports, Nagios provides real-time insights into the health and performance of infrastructure components, enabling stakeholders to make informed decisions and take timely actions. Nagios is highly scalable and adaptable to diverse IT environments, offering flexibility in deployment and configuration. Administrators can tailor monitoring configurations to suit their specific requirements, defining custom checks, thresholds, and notifications. This level of customization ensures that Nagios can monitor virtually any aspect of an IT environment, providing granular insights into system performance and behavior. By proactively monitoring infrastructure components, Nagios helps improve the reliability and availability of IT services, minimizing service outages and maximizing uptime. Nagios aids organizations in achieving regulatory compliance and enhancing security posture by monitoring critical security parameters and adherence to industry standards. By leveraging Nagios' capabilities, organizations can optimize system performance, mitigate risks, and maintain a resilient IT infrastructure in today's dynamic digital landscape.

FAQ (Preguntas y respuestas)
=================

### Q1: Is Nagios difficult to set up and configure?
A1: While Nagios may have a learning curve for beginners, its setup and configuration are well-documented, and there are numerous resources available online to guide users through the process. With patience and perseverance, users can effectively deploy Nagios to meet their monitoring needs.

### Q2: Can Nagios monitor both physical and virtual infrastructure?
A2: Yes, Nagios can monitor both physical and virtual infrastructure. Whether it's servers, networks, applications, or services, Nagios offers the flexibility to monitor a wide range of components across diverse IT environments, including virtualized infrastructure deployed on platforms like VMware or Hyper-V.

### Q3: What types of alerts can Nagios send in case of issues?
A3: Nagios can send various types of alerts, including email notifications, SMS messages, and SNMP traps, among others. Administrators can customize alerting rules based on predefined thresholds or specific conditions, ensuring that they receive timely notifications when issues arise within their infrastructure.

### Q4: Is Nagios open source and free to use?
A4: Yes, Nagios is open source software distributed under the GNU General Public License (GPL). This means that it is free to use, modify, and distribute, making it accessible to organizations of all sizes and budgets. Additionally, there are commercial versions and plugins available for users who require additional features and support.

### Q5: Can Nagios integrate with other monitoring tools and systems?
A5: Yes, Nagios supports integration with a wide range of third-party tools and systems through its extensible architecture and robust APIs. Whether it's integrating with ticketing systems, logging solutions, or cloud platforms, Nagios can seamlessly communicate and share data with other monitoring and management tools, enhancing overall operational efficiency and visibility.

### Contacts

* saltamara@itsa.edu.co
* Jbarrazam@itsa.edu.co

### Acknowledgements 
* Tutorial: https://tecnolitas.com/blog/como-instalar-nagios-en-ubuntu-20-04/
* Nagios. Website: [Nagios Documentation](https://www.nagios.org/documentation/)
* Linux Academy: https://www.youtube.com/channel/UClGShptNEuvTWGAAfpa2Etw


