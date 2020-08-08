# Automating django deployment with Ansible

1. Add real ip address in hosts.yml and rename file name in host_vars with that address.
2. Add `.env` file to templates folder with the following content:
```dotenv
DATABASE_URL=postgres://{{ project_db_user_name }}:{{ project_db_user_password }}@127.0.0.1:5432/{{ project_db_name }}
DJANGO_DEBUG=False
DJANGO_SECRET_KEY=secret-pass
REDIS_URL=redis://127.0.0.1:6379/1
DJANGO_ADMIN_URL='admin/'
DJANGO_ALLOWED_HOSTS="127.0.0.1,0.0.0.0,localhost,84.38.182.166"
EMAIL_BACKEND='django.core.mail.backends.console.EmailBackend'
```

3. Add `project_vars.yml` filt to vars folder:
```yaml
---
deploy_user_name: django_user
project_dir_name: rfrit
project_dir_path: "/home/{{deploy_user_name}}/sites/{{project_dir_name}}/"
project_db_name: rfrit_db
project_db_user_name: rfrit_db_user
project_db_user_password: password-asdasd
repository_url: repo_url
git_username: John Doe
git_email: j.doe@gmail.com
host_ssh_file_path: "/home/{{deploy_user_name}}/.ssh/id_rsa"
env_file_src_path: ../templates/.env
env_file_dest_path: "{{ project_dir_path }}"
```
