

# Notes for centos 2009 in lab

vi /etc/yum.d.repos/CentOS-Base.repo

for [base] 
baseurl=http://vault.centos.org/7.9.2009/os/$basearch/
for [updates]
baseurl=http://vault.centos.org/7.9.2009/updates/$basearch/
for [extras]
baseurl=http://vault.centos.org/7.9.2009/extras/$basearch/
