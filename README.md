ansible.s3.replicated
=========

Creates 2 buckets and configures replication within a single account. 

Requirements
------------

aws cli

Role Variables
--------------

`appname: ` - Used for tagging and default naming of policies

`env: ` - Used for default tagging

`owner: ` - Used for default tagging. Email address for team that owns the resource

`account_name: ` - AWS Account Name

`account_number: ` - AWS Account Number

`source_bucket_name: `

`source_bucket_region: us-east-1`

`destination_bucket_name: ` - must be in a different region from source bucket

`destination_bucket_region: us-west-2`

`enable_bucket_logging: false` - Enable s3 access logs

`logging_bucket: "{{ account_name }}.logs` - Target for the buckets to log to

`logging_bucket_prefix: s3logs/`

`iam_role_name: "{{ appname }}-s3-replication-role"` - name of the iam role created for replication. IAM steps are manual

`iam_policy_name: "{{ appname }}-s3-replication-policy"` - name of the iam policy for replication. IAM steps are manual

`iam_role_arn: arn:aws:iam::{{ account_number }}:role/acct-managed/{{ iam_role_name }}` - arn of the policy to attach to the bucket

```
tags:
  app: "{{ appname }}"
  env: "{{ env }}"
  buildtype: Ansible
  owner: "{{ owner }}"
  tier: data
```

Dependencies
------------



Example Playbook
----------------

    - hosts: localhost
      vars:
        appname: myapp
        env: production
        owner: user@example.com
        account_name: awsacctabc
        account_number: 123456789
        source_bucket_name: mysourcebucket
        destination_bucket_name: mydestinationbucket
      roles:
         - { role: ansible.s3.replicated }

License
-------

BSD

Author Information
------------------

stewie.zc@gmail.com
