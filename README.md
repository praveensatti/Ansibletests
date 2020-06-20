###Readme###

##ansible.cfg
#ansible config file
[defaults]
inventory = ./inventory
remote_user = praveen_s
private_key_file = /imihome/praveen_s/id.rsa
host_key_checking = False


##inventory
#few test servers
[mosca]
172.16.29.14
172.16.29.73
