```
git clone https://ShunTr@bitbucket.org/primate_vault/beeclock.git
mv ./paymeter/* ./
mv ./paymeter/.[!.]* ./
rm -R paymeter/
chown -R paymeter:psacln ./
chown paymeter:psaserv ./
git ls-remote
git add .gitignore
git add .
git commit -m "initial commit of full repository"
git push -u origin master
chmod +x git_automatic_commit.run
/var/www/vhosts/paymeter.primate.es/httpdocs/git_automatic_commit.run
```