Please run this ansible script as described below to see the error I encounter about WeaverEmailService.

For this test the script is set to run without shibboleth and without SSL.  Note that the smtp settings
in application.yml are set to test for this deploy (I set them for institutional deployments) but this
is not relevant to the error.

This ansible script will create a base install of vireo4 on a VM.  The file 'Vagrantfile'
denotes the base image for an amazon linux 2 deployment with the setting:
      override.vm.box = "gbailey/amzn2"
AMZN linux 2 is what TDL uses for deployment on the new vireo4 servers for member institutions.



Install vagrant and ansible.
	(I'm running ansible 2.9.9 and vagrant 2.2.7)

Clone this repository.

Make sure port 8080 is free on your computer.  If not you may need to change port settings in Vagrantfile.

Edit the vars_vireo4.yml file so that branch 4.1.0_nov2020 is built:
```
vireo_gitbranch: 4.1.0_nov2020
```

Build vireo in a virtual machine:
```
vagrant up
```

After a few minutes the script will conclude.

Confirm that vireo4 is properly running at http://localhost:8080

Stop the VM with the destroy command (it will ask for confirmation):
```
vagrant destroy
```

Edit the vars_vireo4.yml file so that branch 4.1.0 will now be built:
```
vireo_gitbranch: 4.1.0
```

Rebuild vireo in a virtual machine:
```
vagrant up
```

Clear browser cache and confirm that localhost:8080 does not bring up vireo4.

Sign in to VM to inspect: 
```
vagrant ssh
```

Sign in as vireo4
```
sudo bash -login
```

Inspect /ebs/vireo/logs/ and note that vireo4 didn't even get around to producing an application.log file

Stop vireo4
```
service vireo4 stop
service vireo4 status
```

Sign in as vireo4 and run it manually
```
sudo -u vireo4 bash -login
cd ~/etd/Vireo/
java -jar target/vireo-4.1.0.war
```
See error:
	
	***************************
	APPLICATION FAILED TO START
	***************************
	
	Description:
	
	Field emailSender in org.tdl.vireo.service.SubmissionEmailService required a bean of type 'edu.tamu.weaver.email.service.WeaverEmailService' that could not be found.
	
	
	Action:
	
	Consider defining a bean of type 'edu.tamu.weaver.email.service.WeaverEmailService' in your configuration.
	
	2020-11-24 16:23:25.602 ERROR 26768 --- [           main] o.s.b.d.LoggingFailureAnalysisReporter   : 





