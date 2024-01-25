С помощью Vagrant была поднята ВМ nginx.

Ansible playbook делает ряд действий на ВМ:
 1) обновляет пакеты
 - name: update
      apt:
        update_cache=yes
      tags:
        - update apt
 2) скачивает веб сервер ...
  - name: Install nginx
      apt:
        name: nginx
        state: latest
      notify: 
        - restart nginx
      tags: 
        - nginx-package

 3) меняет конфигурацинный файл по шаблону 
  - name: NGINX | Create NGINX config file from template
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/sites-enabled/default
      notify: 
        - reload nginx
      tags:
        - nginx-configuration
 4) перезапускает сервер и перечитывает конфигурацию
 handlers:
    - name: restart nginx
      systemd:
        name: nginx
        state: restarted
        enabled: yes

    - name: reload nginx
      systemd: 
        name: nginx
        state: reloaded
