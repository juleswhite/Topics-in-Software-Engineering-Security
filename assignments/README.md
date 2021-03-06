# Assignment 1

## Due Date

This assignment is due before the first live session. Please email the instructor if you have trouble with the assignment.

## Instructions 

This assignment requires a lot of development environment set up work. You should start early. Almost all future assignments will build off of this set up work. Future assignments will assume and require that you completed this assignment successfully.

Look at the announcements in the course learning management system for the link to the codegen.jar file.

Complete all of the steps listed below and then submit the items listed in the last step.

1. Download and install Eclipse (https://www.eclipse.org/) and Google Chrome
2. Install the Eclipse M2E plugin: https://www.eclipse.org/m2e/ or from the Marketplace: https://marketplace.eclipse.org/content/maven-integration-eclipse-luna-and-newer
Clone the Git repository: git@github.com:knowm/XDropWizard.git
Remove the following lines from the pom.xml file:

```
<!--for Java code formatting -->
 <plugin>
   <groupId>com.coveo</groupId>
   <artifactId>fmt-maven-plugin</artifactId>
   <version>2.9</version>
   <configuration>
     <filesNamePattern>.*\.java</filesNamePattern>
     <skip>false</skip>
   </configuration>
   <executions>
     <execution>
       <goals>
         <goal>format</goal>
       </goals>
     </execution>
   </executions>
 </plugin>
```
3. Import the project into Eclipse using File->Import->Maven->Existing Maven Projects
4. Create a new Java Application run configuration that passes the arguments "server xdropwizard.yml" to the main class: "org.knowm.xdropwizard.XDropWizardApplication"
5. Run the new configuration and make sure that you can access http://localhost:9090
6. Stop the configuration in the console by hitting the red square
7. Clone the Git repository: https://github.com/spring-projects/spring-petclinic
8. Import the project as an existing Maven project into Eclipse
9. Create a new run configuration for the main class: "org.springframework.samples.petclinic.PetClinicApplication" (no arguments)
10. Run the new configuration and make sure that you can access http://localhost:8080
11. Stop the application
12. Install VirtualBox (old versions can cause issues)
13. Install Vagrant
14. Create a directory called "asgn0"
15. Inside the directory, Create a Vagrantfile with these contents:

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/xenial64"
  config.vm.provision :shell, path: "provision.sh"
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
```
16. In the same directory as the Vagrantfile, create a "provision.sh" file with executable permissions and these contents:
```
# Set up a shared directory for logs
mkdir /vagrant/logs

# Update the package manager and install basics
sudo apt-get update 
sudo apt-get install -y software-properties-common
sudo apt-get install -y python-software-properties
sudo apt-get install -y add-apt-repository
sudo apt-get install -y curl

# Install ZeroTier
curl -s 'https://raw.githubusercontent.com/zerotier/download.zerotier.com/master/htdocs/contact%40zerotier.com.gpg' | gpg --import && \
if z=$(curl -s 'https://install.zerotier.com/' | gpg); then echo "$z" | sudo bash; fi
sleep 5
sudo zerotier-cli info > /vagrant/logs/zerotier-status.txt
sudo zerotier-cli join 83048a063202620b

# Install the JDK
sudo apt-get install -y default-jdk
java -version 2> /vagrant/logs/java-status.txt

# Install Node
sudo apt-get install -y nodejs
nodejs -v > /vagrant/logs/node-status.txt

# Install Docker
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
sudo docker run hello-world > /vagrant/logs/docker-status.txt
```
17. Start the VM with "vagrant up"
18. When it finishes booting, "vagrant ssh" to access the VM
19. Type "exit" to close the Vagrant SSH connection
20. You should have a series of logs that were produced in "logs"
21. Download the codegen.jar file attached to this assignment
22. Create a new directory to hold the contents of a randomly generated Java web application
23. Run the codegen.jar with the command "java -jar codegen.jar -d \<full path to the directory you created\>"
24. Follow the instructions that print after the code generator finishes running (this will include installing and running JHipster)
25. Submit a zip file with the following: 
    1. a screenshot of the browser after it has loaded your XDropwizardApplication on http://localhost:9090
    2. a screenshot of the browser after it has loaded your Spring Pet Clinic application on http://localhost:8080
    3. a screenshot of both projects imported into Eclipse
    4. the folder for the logs directory produced by Vagrant
    5. a folder that contains the generated source for your JHipster application but DOES NOT INCLUDE the node_modules, .git, .gradle, or build directories,  (make sure that the .yo-rc.json file and the .jhipster folder).

# Assignment 2

This assignment is officially released.

## Due Date

This assignment is due five hours before the fifth live session.

## Overview

An important component of software security is learning to identify vulnerabilities in source code, development processes, usage, and other software aspects. Developers gain exposure to vulnerabilities through their career by seeing vulnerabilities in peer code, learning about vulnerabilities in software, and receiving feedback about vulnerabilities in their own code. Building up experience to be able to effectively spot and fix key vulnerabilities takes time.

This assignment is designed to help you to learn the patterns of vulnerabilities in different software aspects by exposing you to both the creation and identification of vulnerabilities in a variety of code bases. You will both produce demonstrations of real vulnerabilities and try to identify the vulnerabilities created by others. Both production and identification of vulnerabilities can be deceptively challenging - do not understimate the difficulty of this assignment.

## Vulnerabilities to Demonstrate
For this assignment, you need to demonsrate at least two injection attack vulnerabilities.

## Vulnerability Secrecy
You are required to keep your vulnerability demonstration secret until after it is discussed in class. You may not discuss your vulnerability with any of your peers prior to the due date.

## The Code
You can demonstrate the vulnerabilities in the web application code base of your choice. You have also being provided a code generator that will generate a semi-random Java web application. The code generator is the one that you used in the first assignment. You can either use a web application code base of your choosing or the generated code as the basis of your solution. You are free to use one of the code bases that you generated in the first assignment as the basis of this one. 

## Documenting Your Vulnerability
After you have modified the application to create your injection vulnerability, you must document your vulnerability. You must document the vulnerability using the format shown below in a file named vulnerability.md. You should edit the example below to be specific to your code base and vulnerability. You MUST include sample instructions for exploiting the vulnerability via curl. You must describe why the vulnerability is an issue and what to look for in the output of your curl command.

```
# Overview 
This code base demonstrates the following attacks: ....

# Vulnerability 1: Injection Attack

The code includes an injection attack that allows an attacker to inject arbitrary
commands into the server via Java's Runtime.exec() mechanism. The vulnerable code
path is as follows:

1. HTTP requests sent to the Foo controller's getBar() method accept a "q" parameter
   on lines 183-192
2. The "q" parameter is concatenated with a String to set the value for the "f" variable
   on line 195
3. The "f" variable is passed to Runtime.exec() on line 197

The vulnerability can be exploited by following the steps below:

1. Using curl, send the following request to the server:
   
   curl -XGET http://localhost:8080/foo/bar -d '; ls'
   
2. The server should send back a String that includes a list of the files in the 
   directory where the server is running, including an entry for "build.gradle", which
   is a sensitive internal file.
3. Arbitrary commands could be substituted for the "q" parameter allowing attacks on 
   the server

# Vulnerability 2: ....
  ...
```

## Submission
To hand-in your assignment, please submit a zip file that includes your vulnerability.md file and your project WITHOUT any binary directories (e.g., bin, build, node_modules, etc.).

## Grading
The grade will be based on the following components:

Each vulnerability demonstration will be assessed based on the following criteria:

 - (20pts) The vulnerability listed is correctly demonstrated
 - (20pts) The vulnerability demonstration is well integrated into the functionality of the application
 - (10pts) The vulnerability is correctly documented in the vulnerability.md file
 - (10pts) The vulnerability can be reproduced from the provided documentation
 - (10pts) The lines of source code that create the vulnerability are described in sufficient detail
 - (30pts) Overall quality of the vulnerability demonstrations and their documentation
 
You should preference high-quality demonstrations with excellent documentation.

# Assignment 3

## Due Date

The assignment is due before the ninth live session. Please send your slides to the instructor at least two hours prior to the live session. 

## Instructions
Identify a piece of software, system, human process, set of instructions, etc. that you think demonstrates excellent design with respect to security. You do not have to restrict yourself to software. Prepare a 5-7min presentation on the system and an associated set of slides. Make sure and explain why the thing that you present demonstrates good security design and relate its design choices back to what is discussed in the course. Please send your slides to the instructor at least two hours prior to the live session. 

# Assignment 4

## Due Date

The assignment is due before the tenth live session. Please send your slides to the instructor at least two hours prior to the live session. 

## Instructions
Identify three security incidents where poor design played a role. Prepare a 5-7min presentation on the incidents, the associated design flaws (not implementation flaws), and design changes that would have prevented the problem. Prepare a set of slides to accompany your presentation. Make sure and explain why the things that you present demonstrate problems with design as opposed to implementation, deployment and confgiuration, usage, etc.. Please send your slides to the instructor at least two hours prior to the live session. 


# Final Project

Your goal for the final project is to help improve cyber-security at
Vanderbilt. Your project can be anything that requires substantial
thought and work. Projects can be anything ranging from writing a new
software tool to developing training materials to designing new
security systems to performing a detailed analysis of something's
security. 

If the project requires significant work and thought related to
security, even if it doesn't fit into one of the categories listed
above, it can be approved by the instructor. The role of these
examples is to help generate ideas and not constrain what you can
do. The only hard requirement is that the instructor must approve the
idea after your idea presentation. If the project does not meet the
requirements, the instructor will ask you to change ideas.

Whatever project that you choose, you must have good answers to the
Heilmeier Questions:

 * What are you trying to do? Articulate your objectives using
      absolutely no jargon.
  * How is it done today, and what are the limits of current
      practice?
  * What is new in your approach and why do you think it will be
      successful?
  * Who cares? If you are successful, what difference will it make?
  * What are the risks?
  * How much will it cost? If your approach isn't free, think
      carefully about the cost to use or implement what you propose.
  * How long will it take?
  * What are the mid-term and final “exams” to check for success?

The deliverables for your project are as follows:

 1. You will deliver a presentation on your idea in the eleventh sync session. Your presentation
    should be ~5mins long. Make sure and explain your project clearly. You should be prepared
    to ask questions about other students' project ideas and answer questions
    about your own project idea.
 2. You must present your project in at most 7mins in the last sync session.
 3. You will create final video (1-3mins) that clearly explains your project and is targeted 
    at the general public
 4. If you produce a software tool as part of your project, you
    must demo it as part of your final presentation.
