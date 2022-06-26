  
  
JANUSEC Privacy Installation and User's Guide  
   
Table of Contents  
1.  [Installation](#installation)    
1.1 [System Requirements](#system-requirements)      
1.2 [Installation Steps](#installation-steps)      
2.  [Initial Configuration](#initial-configuration)      
2.1 [Admin Login](#admin-login)     
2.2 [Organization](#organization)    
2.3 [Data Classification](#data-classification)    
2.4 [Applicable Laws](#applicable-laws)    
2.5 [Assessment Templates](#assessment-templates)    
2.6 [Users Management](#users-management)    
2.6 [Global Settings](#global-settings)    
3.  [Record of Processing Activities](#record-of-processing-activities)    
4.  [Privacy Impact Assessment (PIA)](#privacy-impact-assessment-pia)     
5.  [Prepare for Inspection or Audit](#prepare-for-inspection-or-audit)     
6.  [Prepare to Report](#prepare-to-report)    
7.  [Subscription](#subscription)    
8.  [Support](#support)    
  
   
#  Installation  
  
##  System Requirements    
  
JANUSEC Privacy adopts on-premise deployment. System requirements:    
* Operating System: Debian 9/10/11+, AMD64 (or X86-64)    
* Database: PostgreSQL 10/11/12/13+  
* RAM: 2GB+  

## Installation Steps  

Step 1: Install PostgreSQL (if PostgreSQL is ready, skip this step)  
Switch to root user, and run command:  
> #apt install postgresql  
  
Step 2: Switch to postgres and create database and user  
> #su - postgres  
> $psql  
> =>create user janusecprivacy with password 'J@nusec123';  
> =>create database janusecprivacy owner janusecprivacy;  
> =>grant all privileges on database janusecprivacy to janusecprivacy;  
> =>\q  
> $exit  

Then test the database connection:  
> $psql -h 127.0.0.1 -U janusecprivacy -W janusecprivacy  

Note: Database name and user name cannot include minus sign '-' .  

Step 3: Check database connection  
> $psql -h 127.0.0.1 -U janusecprivacy -W janusecprivacy  

Input password (J@nusec123 In the above example), if you see:  
> janusecprivacy=>  

Test OK, input \q exit the console.  
  
Step 4: Install JANUSEC Privacy  
> #tar -zxf janusec-privacy.tar.gz  
> #cd janusec-privacy  
> #./install.sh  

It will be installed to `/usr/local/janusec-privacy/`  
  
Step 5: Modify config.json and start service  
> #cd /usr/local/janusec-privacy/  

Then use vi or other editor to edit config.json:  
```
{  
        "site": {  
                "debug": false,  
                "listen_http": ":8088",  
                "listen_https": ":8443",  
                "certificate": "/path/to/public.pem",  
                "certificate_key": "/path/to/private.key",  
                "force_https": false  
        },  
        "database": {  
                "host": "127.0.0.1",  
                "port": "5432",  
                "user": " janusecprivacy",  
                "password": "J@nusec123",  
                "dbname": " janusecprivacy "  
        }  
}  
```

If no HTTPS required, then set listen_https to empty string:  
> "listen_https": ""  

If the length of password is less then 32bits, it will be encrypted automatically. The encrypted password can be modified by new password if the password was changed.  
  
Step 6: Start janusec-privacy.service and check its status  
> #systemctl start janusec-privacy  
> #systemctl status janusec-privacy  

The result should like the following:  
```
janusec-privacy.service - Janusec Privacy Compliance Governance
   Loaded: loaded (/lib/systemd/system/janusec-privacy.service; enabled; vendor preset: disabled)
   Active: active (running) since Sun 2022-06-19 12:46:22 CST; 1 weeks 0 days ago
     Docs: https://www.janusec.com/
 Main PID: 20818 (bash)
   CGroup: /system.slice/janusec-privacy.service
           ├─20818 /bin/bash -c /usr/local/janusec-privacy/janusec-privacy >> /usr/local/janusec-privacy/log/error.log ...           └─20819 /usr/local/janusec-privacy/janusec-privacy
```
   
If the status of this service is enabled and active (running), it means JANUSEC Privacy successfully run, otherwise you need check the `/usr/local/janusec-privacy/log/error.log` and `config.json` .  
  
# Initial Configuration    
  
## Admin Login  

First, login the system `http://Domain_or_IP_Address:8088/` , the port number should be consistent with the configuration file (`/usr/local/janusec-privacy/config.json`).  
Please use username `admin` and password `J@nusec123`.  
   
After the first login, modification the password for admin is required:  
   
As an alternative method, an Email code can be used to log in.  

## Organization  

Under Configuration -> Organization, complete all the legal entities, business groups, and multinational management organization.  
   
Note:  
* Organization shall be configured before this system open to other employees.   

## Data Classification  

Review the data classification and data rating.   
   
Especially, modify the data rating according to the internal policy of your company.  
   
## Applicable Laws  

European GDPR and China Personal Information Protection Law are preset. If there are other applicable laws, please add them.  
   
Take GDPR as an example, fill the basic information:  
   
Legal bases for processing personal data:  
   
Condition of processing sensitive personal data:  
   
Legal roles:  
   
And transfer mechanisms:  
   
## Assessment Templates  

Some typical templates were preset by JANUSEC Privacy, if other templates are required, please add to this list.  
   
## Users Management  

Add users and set their roles.
   
   
## Global Settings  

For security purpose, Email suffix should be limited.  

Configure SMTP for sending reminders and to-dos.  
   
Configure Retention period (example: 1826 days, i.e., 5 years) for automatic cleanup of expired data.   
   
Now you can invite them to use this system by sent the URL.  

# Record of Processing Activities  

Now, switch to a business unit perspective.  
Under Inventory -> Processing Activities, click "Add Processing Activity":  
   
Add data fields processed by this activity:  
   
Finish the internal sharing and external disclosure to third parties:  
   
Then it will produce data flow diagram automatically:  
   
# Privacy Impact Assessment (PIA)  

Under Risk Assessment of each processing activity (or asset, or external recipients), assessments may be created.  
   
Click the assessment name, enter into the details page:  
   
Each assessment has four stages: Initial, Review, Approval, and Done.  
* Initial: the first stage, the business representative fills in the questionnaire.  
* Review: the second stage, the PO (Privacy Officer) review the questionnaire and add comments.  
* Approval: the third stage, the business executive approve or reject the assessment according to the opinion of the PO.  
* Done: Finished status, read only.  

# Prepare for Inspection or Audit  

When prepare for inspection or audit, processing activities and assessments may be exported as pdf files, as input and compliance evidences to an inspection or audit.   

# Prepare to Report  

Under menu Dashboard, operation data is available:  
   
# Subscription  

One-month free subscription is preset when JANUSEC Privacy is installed.  
If no more subscription when it expires, JANUSEC Privacy will be read only.  
Subscription is available by monthly or yearly, please refer to https://www/janusec.com/pricing for more information.  

# Support  

Online Support: https://www.janusec.com/tickets/new   
Email: support at janusec dot com  
Official Site: https://www.janusec.com   
  