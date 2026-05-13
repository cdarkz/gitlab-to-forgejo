# Gitlab to Forgejo migration script

## Preamble

This script uses the Gitlab API and a combination of [pyforgejo](https://codeberg.org/harabat/pyforgejo) and python `requests` to migrate all data from Gitlab to Forgejo.

This script supports migration of:

* Repositories & Wiki (fork status is lost)
* Users (no profile pictures)
* Groups
* Public SSH keys

Tested with Gitlab Version 17.2.1 and Forgejo Version 8.0.0

Tested with Gitlab Version 18.11.0 and Forgejo Version 14.0.3 for project only mode

### Forgejo notice
If you are using Nginx to proxy to Forgejo, it's recommended to extend the timeout.
```
location / {
    proxy_read_timeout 300;
    proxy_connect_timeout 300;
    proxy_send_timeout 300;
    ...
}
```

## Usage

### How to use with venv

To keep your local system clean, it is preferrable to use a virtual environment.
You can follow these steps:

```bash
python3 -m venv migration
source migration/bin/activate
python3 -m pip install -r requirements.txt
```

and you call the scripts using `--help`:

* `./migrate.py --help`
* `./create_push_mirrors.py --help`

### ini file

You need to create a configuration file called `.migrate.ini` and store it in the same directory of the script.  
:bulb: `.migrate.ini` is listed in `.gitignore`.

```ini
[migrate]
gitlab_url = https://gitlab.example.com
gitlab_token = <your-gitlab-token>
gitlab_admin_user = <gitlab-admin-user>
gitlab_admin_pass = <your-gitlab-password>
forgejo_url = https://forgejo.example.com
forgejo_token = <your-forgejo-token>
forgejo_admin_user = <forgejo-admin-user>
forgejo_admin_pass = <your-forgejo-password>
```

### Credits and fork information

This is a fork of [gitlab_to_gitea](https://git.autonomic.zone/kawaiipunk/gitlab-to-gitea.git), with less features (this script does not import issues, milestones and labels)
