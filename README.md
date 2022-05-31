# installation template

### eric o meehan
### 2022-05-19

## description
template for automated and source controlled arch linux installations

this repository is a template designed to be cloned and edited to create new installations
installations are intended to be ephemeral - reprovisiioned rather than updated

## usage
1. fork the template repository to $gitServer:installations/$installationId
2. edit the repository contents to define the desired installation:
	* list packages to be installed, services to be enabled, and the timezone in their respective files
	* add executables and configuration files to bin and etc respectively
		- nest files within any necessary directories, i.e.:
			```
			hosts
			fstab
			ssh/sshd
			```
		- add these paths to the respective 'index.log' file
	* define groups, users, and policies in separate repositories
	* add groups, users, and policies to the installation as git submodules:
		- installations may contain groups, users, and policies
		- groups may contain users and policies
		- users may contain policies
3. format drives and mount to a filesystem rooted at /mnt/$installationId
4. put fstab under source control:
	```
	genfstab -U /mnt/$installationId >> $gitServer:installations/$installationId/etc/fstab
	git commit ...
	```
5. execute the configuration script:
	```
	./install
		-e|--executionId	id to tag logs		default: generated at start
		-g|--gitServer		specify a git server	default: localhost
		-s|--syslogServer	remote syslog server	default: local syslog
	```
