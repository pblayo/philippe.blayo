Commands used by Philippe Blayo

# Dataverse : survey's data warehouse

```$ git remote -v
origin	https://github.com/IQSS/dataverse.git (fetch)
origin	https://github.com/IQSS/dataverse.git (push)
pblayo	git@github.com:pblayo/dataverse.git (fetch)
pblayo	git@github.com:pblayo/dataverse.git (push)
```

`./initial.bash`
`docker-compose up`
Access through http://localhost:8085

- To log in as root, the username is *dataverseAdmin*, the password is *admin*

- Create a new user.
Problem : I don't receive the confirmation's email. It should have been sent to my personnal adress.

With a Google search of "site:guides.dataverse.org email"


> I tried to find out if there was something to configure in the dataverse documentation.
> Unfortunately for developers not at Harvard, the installer script gives you by default an SMTP server of mail.hmdc.harvard.edu but you can specify an alternative SMTP server when you run the installer.

[1] http://guides.dataverse.org/en/latest/developers/troubleshooting.html

## Interesting entries in documentation

http://guides.dataverse.org/en/latest/user/account.html
http://guides.dataverse.org/en/latest/installation/oauth2.html
