> **This page is community content**





In a lot of groups are advices not to run the new UI on a public server, below is a small how to, to protect your UI with a password behind the proxy. 

First of we to install nginx depends on your operation system, in this case we use debian/ubuntu.

`sudo apt install nginx`

then you navigate to /etc/nginx/site-enable/ with

`cd /etc/nginx/sites-enabled`

`vi default`
remove everything inside and replace it with

server {
    listen 80;

    server_name your_hostname;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        auth_basic "Restricted Content";
        auth_basic_user_file /etc/nginx/.htpasswd;
    }
}

Create the Password File
To start out, we need to create the file that will hold our username and password combinations. You can do this by using the OpenSSL utilities that may already be available on your server. Alternatively, you can use the purpose-made htpasswd utility included in the apache2-utils package (Nginx password files use the same format as Apache). Choose the method below that you like best.

Create the Password File Using the OpenSSL Utilities

If you have OpenSSL installed on your server, you can create a password file with no additional packages. We will create a hidden file called .htpasswd in the /etc/nginx configuration directory to store our username and password combinations.

You can add a username to the file using this command. We are using sammy as our username, but you can use whatever name you'd like:


`sudo sh -c "echo -n 'miwi:' >> /etc/nginx/.htpasswd"`
Next, add an encrypted password entry for the username by typing:


`sudo sh -c "openssl passwd -apr1 >> /etc/nginx/.htpasswd"`
You can repeat this process for additional usernames. You can see how the usernames and encrypted passwords are stored within the file by typing:

`cat /etc/nginx/.htpasswd`
Output
`miwi:$apr1$wI1/T0nB$jEKuTJHkTOOWkopnXqC1d1`


Create the Password File Using Apache Utilities

While OpenSSL can encrypt passwords for Nginx authentication, many users find it easier to use a purpose-built utility. The htpasswd utility, found in the apache2-utils package, serves this function well.

Install the apache2-utils package on your server by typing:

`sudo apt-get install apache2-utils`
Now, you have access to the htpasswd command. We can use this to create a password file that Nginx can use to authenticate users. We will create a hidden file for this purpose called .htpasswd within our /etc/nginx configuration directory.

The first time we use this utility, we need to add the -c option to create the specified file. We specify a username (miwi in this example) at the end of the command to create a new entry within the file:

`sudo htpasswd -c /etc/nginx/.htpasswd miwi`
You will be asked to supply and confirm a password for the user.

Leave out the -c argument for any additional users you wish to add:

`sudo htpasswd /etc/nginx/.htpasswd another_user`
If we view the contents of the file, we can see the username and the encrypted password for each record:

`cat /etc/nginx/.htpasswd`
Output

`miwi:$apr1$lzxsIfXG$tmCvCfb49vpPFwKGVsuYz.`
`another_user:$apr1$p1E9MeAf$kiAhneUwr.MhAE2kKGYHK.`

Please replace the username miwi with your own username.

Have fun!