
# Identify and Characterize Security Mistakes

Using news and Internet articles, find examples of real security incidents (e.g., the Equifax data breach) for each type of usage mistake in the videos. Once you have found a real-world security incident stemming from each type of mistake, write a 2-paragraph (or more if you choose) summary of the incident that describes what happened, specifies how that type of mistake manifested in the incident, and includes what the impact of the incident was.

# Identify Examples of Common Development Mistakes

Using news and Internet articles, find examples of real security incidents (e.g., the Equifax data breach) for 5 different types of development mistakes. Once you have found a real-world security incident stemming from each type of mistake, write a 2-paragraph (or more if you choose) summary of the incident that describes what happened, specifies how that type of mistake manifested in the incident, and includes what the impact of the incident was.

# Viewing HTTPS Certificate Details
Find 3 websites that use HTTPS. On each website, using Google Chrome, click on the lock icon next to the "https" in the URL and view the certificate used to secure the connection with the website. For each website that you do this for, list the trust chain (e.g., signers) up to the root.

# Create a Key Pair

Research how to create an RSA key pair on your computer. Generate an RSA key pair in the format of your choosing and post the public key.

# Identify Session IDs

Log into Vanderbilt's YES system. Open the Chrome Developer Tools with View->Developer->Developer Tools. Click on the Application tab and look for the Cookies listed under Storage. What do you think the name of the session ID could be? Make sure you DO NOT post the value of any of these.

# Identity

Perform an audit of Vanderbilt's YES application. What are the ways that it establishes identity? What sensitive identity information does it display? What sensitive identity information is embedded in the HTML the application returns? Does the way that YES maintains identity open users up to any types of attack?

You can use Chrome's developer tools to perform this audit. Open YES and go to View->Developer->View Source to view the HTML source. Try searching for words like "id", your name, etc.

# Identify Software & Libraries in Use

Create a catalog of your own software usage. List at least 20 software applications or services that you use and their exact version identifier.  For each software application / service, list the latest known version. For each version that you use, list any known vulnerabilities. If you upgrade an application as a result of this audit, list the version before the upgrade and the vulnerabilities that were present.

In addition to your software list, provide a catalog of the devices in your house or room that include software. For each device, list as many details about the software that it runs, such as OS version. List the latest version for each piece of software. If you do not know, label the device with "unknown threats."

# Risk Self-assessment

Examine the NPM, Ruby, Java, Python, Go, or other libraries installed on your machine. List 10 of these dependencies that you find. For each, list the version number and whether or not there are any known CVEs. Can you guarantee that you do not have any vulnerable libraries on your personal computer with CVEs or that could have executed malicious code?

# Dependency Audit

Your goal is to find an open source project that has at least one dependency with a CVE disclosure. Once you have found a project with a vulnerability in a dependency, submit a 2-3 paragraph description of the project, the dependency, and the vulnerability. Include a link to the project and the CVE.

Alternatively, if you are unable to find a project with a dependency affected by a CVE, you can submit a list of 5 projects that you audited. For each project, provide a link to the project, a link to any  file(s) that specify dependencies, and a list of all dependencies / versions used by the project. You must choose projects that each have at least 10 dependencies.

# Security Audit

Pick a Vanderbilt web application (e.g., YES, People Finder) and analyze the inputs that it receives. Create a catalog of these inputs (who, what, where, when) per the lectures. For each input, how would you sanitize it? Do you believe the input is passed on to other users or systems?  Who can provide each input and under what circumstances (don't forget to consider "anonymous" as an unauthenticated user). 

Your analysis should be done manually and based solely on what you can see visually in the user interface, source of any web pages, or network requests listed in Chrome Developer Tools. Do NOT run any automated tools against any of these services. Do NOT attempt to send malformed or malicious input to the system. Do NOT do anything to disrupt the system. 

Make sure and include 2-3 paragraph overview of the Vanderbilt system that you analyzed and how you performed your analysis. 

# Data Ownership

Analyze Vanderbilt's YES application. What are the core pieces of data that are in the system? Who can read/write each piece of data? Write a design for a role-based access control system for YES. Your description should include roles for all of the different users of YES, ranging from students to administrators.

# Source Code Analysis

Analyze the provided source code and write a report on its security. Is the application secure? Why or why not?

# Source Code Analysis II

Analyze the provided source code and write a report on its security. Is the application secure? Why or why not?

# Identifying Development Mistakes

Using news and Internet articles, find examples of real security incidents (e.g., the Equifax data breach) for each type of development mistake. Once you have found a real-world security incident stemming from each type of mistake, write a 1-2 paragraph (or more if you choose) summary of the incident that describes what happened, specifies how that type of mistake manifested in the incident, and includes what the impact of the incident was.

# Design an Intrusion Detection System

Design a robust intrusion detection system for YES. What would you monitor and how?

Think through how you would detect a wide variety of attacks, such as:

How would you detect an intruder changing grades? 

How would you detect malware being injected into users' browsers? 

How would you detect parents accessing a student's grades with their login credentials?

# Design an Auditing & Logging Framework

Pick a service used to support students at Vanderbilt and design an auditing and logging system for it. What will you log? How will you store it? How would the data that you log be used to identify different types of attacks / threats?

# What Went Wrong?

Pick a cyber-security incident that was reported on in the news that demonstrates one or more of the issue discussed in the lectures. After choosing your cyber-security incident, write an analysis of the forces, design mistakes, etc. that you think led to this vulnerability not being addressed. Your analysis should include at least 1-2 paragraphs providing an overview of the incident, 1-2 paragraphs describing the vulnerability that was exploited, 1-2 paragraphs describing the impact of the attack, and 2-3 paragraphs describing how this weeks lectures relate to the chosen incident.

# Assess Cloud Security

TODO
