sa-dehydrated
=============

[![Build Status](https://travis-ci.org/softasap/sa-dehydrated.svg?branch=master)](https://travis-ci.org/softasap/sa-dehydrated)
[![License: MIT](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)

This role is based on beautiful script https://github.com/lukas2511/dehydrated
This role is drop-in replacement for sa-lets-encrypt

Basic usage example:
```YAML
---
- hosts: dev

  vars:
    - root_dir: "{{ playbook_dir }}"
    - my_domains:
      - {
          names:        "voronenko.net www.voronenko.net",
          nginx_config: "/etc/nginx/sites-available/voronenko_net"
        }

  pre_tasks:
    - debug: msg="Pre tasks section"

  roles:
    - {
        role:              "sa-dehydrated",
        le_domains:        "{{ my_domains }}",
        option_run_once:   True,
        option_setup_cron: True
      }

  tasks:
    - debug: msg="Tasks section"
```

Advanced example:
```
---
- hosts: www

  vars:
    - root_dir: "{{ playbook_dir }}"
    - my_domains:
      - {
          names:        "voronenko.net www.voronenko.net",
          nginx_config: "/etc/nginx/sites-available/voronenko_net"
        }

  pre_tasks:
    - debug: msg="Pre tasks section"

  roles:
    - {
        role: "sa-nginx"
      }
    - {
        role:         "sa-include",
        include_file: "{{ root_dir }}/demosite.yml"
      }
    - {
        role:              "sa-dehydrated",
        le_domains:        "{{ my_domains }}",
        #le_ca:            "https://acme-staging.api.letsencrypt.org/directory",
        dehydrated_version: "0.4.0",
        option_run_once:   True,
        option_setup_cron: True
      }

  tasks:
    - debug: msg="Tasks section"
```

See standalone example in box-example folder.


![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/1.png)

![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/2.png)

![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/3.png)

![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/4.png)

![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/5.png)

![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/6.png)

![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/7.png)

![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/8.png)

![](https://raw.github.com/softasap/sa-dehydrated/master/box-example/docs/9.png)


Usage with ansible galaxy workflow
----------------------------------

If you installed the sa-dehydrated  role using the command


`
   ansible-galaxy install softasap.sa-dehydrated
`

the role will be available in the folder library/sa-dehydrated

Please adjust the path accordingly.

```YAML

     - {
         role: "softasap.sa-dehydrated"
       }

```




Copyright and license
---------------------

Code licensed under the [BSD 3 clause] (https://opensource.org/licenses/BSD-3-Clause) or the [MIT License] (http://opensource.org/licenses/MIT).

Subscribe for roles updates at [FB] (https://www.facebook.com/SoftAsap/)

Join gitter discussion channel at [Gitter](https://gitter.im/softasap)


