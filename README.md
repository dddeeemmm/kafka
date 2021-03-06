kafka
=========

    Install and config kafka ( standalone | cluster ) + sasl plain

Requirements
------------

    Zookeeper (included, but not use)

Role Variables
--------------

    kafka_install:       true
    kafka_version:       2.6.0
    kafka_version_scala: 2.13
    
    kafka_treads_io:                    16
    kafka_treads_network:               8
    kafka_treads_recovery:              1
    kafka_partitions:                   1
    kafka_buffer_send:                  102400
    kafka_buffer_receive:               102400
    kafka_request_max:                  104857600
    kafka_log_retention_hours:          168
    kafka_log_segment:                  1073741824
    kafka_log_retention_check_interval: 300000
    kafka_zookeeper_connect:            "{% for host in groups ['zookeeper'] %}{{ host }}.{{ domain }}:2181{% if not loop.last %},{% endif %}{% endfor %}"
    kafka_zookeeper_timeout:            18000
    kafka_rebalance_delay:              0
    kafka_bootstrap_servers:            '{% for host in play_hosts %}{{ host }}.{{ domain}}:9092{% if not loop.last %},{% endif %}{% endfor %}'
    
    kafka_sasl:           true
    kafka_sasl_mechanism: PLAINTEXT
    
    kafka_admin_name:     admin
    kafka_admin_password: admin-secret
    
    kafka_users: [] # not required

Dependencies
------------

    Inventory must have group 'zookeeper' or default variable kafka_zookeeper_connect must be reworded

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: kafka }

License
-------

    MIT

Author Information
------------------

    Dmitrij Petrov
