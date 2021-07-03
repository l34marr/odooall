res.users ID 2,6,7 (2=Administrator) seem to match res.partner ID 3,7,8 (3=Administrator)
env.company.name => 'My Company'
env.company.country_id => res.country(227,)

rc = env['res.country']
rc.search_read([('id','=',227)], ['id','name'])
[{'id': 227, 'name': 'Taiwan'}]

https://stackoverflow.com/questions/44158288/odoo-ir-rule-domain-force-for-group-role-depend-on-state

![OWASP top_10](https://miro.medium.com/max/1050/1*tDFmEQnnm-HimaVWiyRAUw.jpeg)
