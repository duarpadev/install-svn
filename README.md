# install-svn

First step, install svn and your components

```apt -y install subversion subversion-tools libapache2-mod-svn lynx```

Create directory to SVN

```mkdir /ssd/svn```

Execute svnadmin to initialize new project

```svnadmin create /ssd/svn/your-repo```

Set permission at user www-data in the path of your project

```chown -R www-data:www-data /ssd/svn/your-repo```

Edit file below with nano and insert block of information inside file <b>dav_snv.conf</b>. After this, save and exit file.

```nano /etc/apache2/mods-enabled/dav_svn.conf```

```

<Location /svn>
     DAV svn
     SVNParentPath /ssd/svn
     AuthType Basic
     AuthName "Subversion Repository"
     AuthUserFile /etc/apache2/dav_svn.passwd
     Require valid-user
</Location>

```

Execute command below

```htpasswd -cm /etc/apache2/dav_svn.passwd user```

<br>NOTICE: Insert line below at file in the last line. Save and exit file.</br>

File dir= /etc/apache2/apache2.conf

```AcceptFilter http none```


Restart Apache to finish process installation of SVN Server

```systemctl restart apache2```
