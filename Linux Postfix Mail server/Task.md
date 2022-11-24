xFusionCorp Industries has planned to set up a common email server in Stork DC. After several meetings and recommendations, they have decided to use postfix as their mail transfer agent and dovecot as an IMAP/POP3 server. We would like you to perform the following steps:

Install and configure postfix on Stork DC mail server.

Create an email account ammar@stratos.xfusioncorp.com identified by B4zNgHA7Ya.

Set its mail directory to /home/ammar/Maildir.

Install and configure dovecot on the same server.

Solution: 

1. Install postfix using: 
    yum install postfix -y

2. Configure postfix by editing the following fields 
    vi /etc/postfix/main.cf
    myhostname = smtp.example.local
    mydomain = stratos.xfusioncorp.com
    myorigin = $mydomain
    inet_interfaces = all
    inet_protocols = all
    mydestination = $myhostname, localhost.$mydomain, localhost,
    mynetworks = 192.168.1.0/24, 127.0.0.0/8( As per your ip range )
    home_mailbox = Maildir/
3. Enable and restart postfix 
    systemctl enable postfix ; systemctl restart postfix

4. add a user 
    useradd ammar@stratos.xfusioncorp.com
    passwd ammar@stratos.xfusioncorp.com
5. Test using :
    telnet localhost smtp
     start transaction using ehlo localhost

     if mail is sent successfully you can check it in 
     ls /home/ammar/Maildir/new/

6. Install Dovecat using 
     yum install dovecot -y

     vi /etc/dovecot/dovecot.conf

     protocols

     vi 
     refer: https://www.digitalocean.com/community/tutorials/how-to-set-up-a-postfix-e-mail-server-with-dovecot 
     or you can edit each files manually

        /etc/dovecot/dovecot.conf
        /etc/dovecot/conf.d/10-mail.conf 
        /etc/dovecot/conf.d/10-auth.conf 
        /etc/dovecot/dovecot-sql.conf.ext 
        /etc/dovecot/conf.d/10-master.conf 
        /etc/dovecot/conf.d/10-ssl.conf 