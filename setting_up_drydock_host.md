# Preparing image:

1. Make sure that `land_queue` code is available in sibling directory.
2. Generate new pair of ssh keys. Prive key will be kept on Phabricator instance and public key on drydock host.
3. Define `.env` file in root directory:

```
PUBLIC_KEY=puthereyourpublickey
```
4. Run `docker-compose build`
5. Run `docker-compose up`
6. Connect to doker container via ssh `ssh phab@127.0.0.1 -p 2222`
7. Open `vim .bash_profile`:
```
eval $(ssh-agent -s)
ssh-add ~/ssh_host_keys/ssh_host_rsa_key
```
7a. `sudo cp .bash_profile /etc/profile`
8. Add public key as `deploy_key` in proper repository
9. Using Phabricators documentation set-up Repository Automation.
10. Test repository automation from Phabricator UI.

## If you are re-running host.
Probably you will encounter some issues, with missing directories (or other things).
1. Do all steps from installation
1. In root directory:
```
mkdir drydock/
sudo ln -s /config/drydock /var/drydock
cd drydock
# you need to check xyz in the failing lease.
mkdir workingcopy-xyz
cd _
mkdir repo
cd _
git clone git@github.com:author/repository
```
