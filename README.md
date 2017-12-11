# Deploy website with git push command

Assuming that your production's files are available in /var/www/html/www.my_website.com

On the server, create a git repository:

    mkdir /var/repos && cd /var/repos
    mkdir my_website.git && cd my_website.git

Initialize the git:

git init --bare

Then we need to create a post-receive hook:

    touch hooks/post-receive
    vi hooks/post-receive

Paste and modify the following lines:

    #!/bin/sh
    GIT_WORK_TREE=/var/www/html/www.my_website.com git checkout --force

Make this file executable:

    chmod +x hooks/post-receive

Now, on your local environment, add your new remote repository:

    git remote add production root@SERVER_IP_ADDRESS:/var/repos/my_website.git
    git push production +master:refs/heads/master

Now every time you need to deploy your application, just run:

    git push production
