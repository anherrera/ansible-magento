## Generic DO Magento Box Vagrant + Ansible

- Requires Ansible 1.2 or newer
- Expects CentOS/RHEL 6.x 

### Getting Started
- Check out this repository.
- Add three directories in the root of this repo (sorry, git won't let me commit empty folders): `public/`, `db/`, and `site-files/`.
- In the `db/` directory, put a gzipped database dump that you would like to use for your local installation. Make sure you remember the name of this file for later. Since this is a vagrant box, usually a pre-stripped dev database works best. This will also cut down on provisioning time.
- In the `site-files/` directory, put your `local.xml` file and your `media/` folder (unzipped). 
- Leave the `public/` directory empty for now. This is where the project root will be.
- You will need to modify `group_vars/all`. Copy the filename of your database dump from earlier and set `mage_db_file` to the file name. Make sure that the database username, password, and database name in `local.xml` match the ones in `group_vars/all` or you won't have a good time.
- The git repo URL needs to be in a specific format. Make sure you include the `username:password@` portion in the URL or the git repo won't check out properly and you won't have a good time. DO NOT COMMIT THIS FILE ONCE MODIFIED. I've seen credentials leaked on github before, trust me, you won't have a good time.
- `cd vm/` and then run `vagrant up`.
- Let vagrant do its thing. If you see an error, shoot a nerf dart at Alexa's head.
- Visit your `server_hostname` in your browser. You should see a magento site, ready to go! If you don't, you either just shot a nerf dart at me, or you're doing this wrong.

----

These playbooks deploy a simple all-in-one configuration of the popular
Magento eCommerce platform, frontend by the Nginx web server and the
PHP-FPM process manager. To use, copy the `hosts.example` file to `hosts` and 
edit the `hosts` inventory file to include the names or URLs of the servers
you want to deploy.

Then run the playbook, like this:

	ansible-playbook -i hosts site.yml

The playbooks will configure MySQL, Magento, Nginx, and PHP-FPM. When the run
is complete, you can access the server to begin the Magento configuration.

### Next Steps / TODO

Ideas for improvement:

- Parameterize the Magento deployment to handle multi-site configurations.
- Separate the components (PHP-FPM, MySQL, Nginx) onto separate hosts and 
hande the configuration appropriately.
- Add support for automatic local / development Vagrant deployment
- Add support for automatic configuration / population of sample / demo products
