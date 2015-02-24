---
title: Using different ssh keys for different hosts
layout: post
published: true
ident: different-ssh-keys-for-different-hosts
---
By default the SSH private key is given the name `id_rsa`  or `id_dsa` and if you try to use a different key and give it another name it wont be detected by SSH command,
you could use the `ssh -i`, but there's a better way -in my opinion at least- to do that
<!-- more -->
you can create `~/.ssh/config` with the following format
{% gist e8bf9cc9acf65d6e656d sample-format.config %}
They don't have to be in any specific order, and any key can be ignored, here's an example after substituting
{% gist e8bf9cc9acf65d6e656d sample-file.config %}
After creating this you can run:  
`ssh myVps`  instead of
`ssh root@11.22.33.44 -P 5432`  
Also keep in mind that you can use in all ssh related commands, like scp for example  `scp myVps:/home/user/file ~/Downloads`  will also work

You can add as much hosts as you could, each with whatever name you want
{% gist e8bf9cc9acf65d6e656d multiple-hosts.config %}
when you run any ssh command it will read the config from the config file and connect to it, not only by name, but if your config partially
match any config in the file, the connection would use the remaining config from the file

Using the last config file, all these connections will work:  
`ssh vps1`,  
`ssh 11.22.33.44`,  
`ssh vpsuser@12.34.56.78`,  
`ssh vps1 -p22`
