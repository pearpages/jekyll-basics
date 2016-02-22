# Deployment Methods

## Automated methods

### Git post-update hook

If you store your Jekyll site in Git (you are using version control, right?), it’s pretty easy to automate the deployment process by setting up a post-update hook in your Git repository, like this:

```bash
$ cat ~/git/blog.git/hooks/post-update 
#!/bin/sh
unset GIT_DIR && cd /home/eugenebolshakov/blog/ && git pull
````

The important thing here is “unset GIT_DIR”. post-update is called by receive-pack that sets GIT_DIR to ‘.’ and confuses “git pull”.

Now I can just add a post, generate the site (_config.yml works great for that), do git push and I’m all set. Nice!

[Read more here](http://www.taknado.com/en/2009/03/26/deploying-a-jekyll-generated-site/)

### Git post-receive hook

To have a remote server handle the deploy for you every time you push changes using Git, you can create a user account which has all the public keys that are authorized to deploy in its authorized_keys file. With that in place, setting up the post-receive hook is done as follows:

```bash
laptop$ ssh deployer@example.com
server$ mkdir myrepo.git
server$ cd myrepo.git
server$ git --bare init
server$ cp hooks/post-receive.sample hooks/post-receive
server$ mkdir /var/www/myrepo
```

Next, add the following lines to hooks/post-receive and be sure Jekyll is installed on the server:

```bash
GIT_REPO=$HOME/myrepo.git
TMP_GIT_CLONE=$HOME/tmp/myrepo
PUBLIC_WWW=/var/www/myrepo

git clone $GIT_REPO $TMP_GIT_CLONE
jekyll build -s $TMP_GIT_CLONE -d $PUBLIC_WWW
rm -Rf $TMP_GIT_CLONE
exit
```

Finally, run the following command on any users laptop that needs to be able to deploy using this hook:

```bash
laptops$ git remote add deploy deployer@example.com:~/myrepo.git
```

Deploying is now as easy as telling nginx or Apache to look at /var/www/myrepo and running the following:

```bash
laptops$ git push deploy master
```
