---
title: Using different ssh keys for different hosts
layout: post
published: true
---
By default the SSH private key is given the name `id_rsa`  or `id_dsa` and if you try to use a different key and give it another name it wont be detected by SSH command,
you could use the `ssh -i`, but there's a better way -in my opinion at least- to do that
<!-- more -->
you can create `~/.ssh/config` with the following format
<script src="https://gist.github.com/coalwater/e8bf9cc9acf65d6e656d.js?file=sample-format.config"></script>
They don't have to be in any specific order, and any key can be ignored, here's an example after substituting
<script src="https://gist.github.com/coalwater/e8bf9cc9acf65d6e656d.js?file=sample-file.config"></script>
After creating this you can run: <br />
`ssh myVps`  instead of
`ssh root@11.22.33.44 -P 5432`,<br />
Also keep in mind that you can use in all ssh related commands, like scp for example  `scp myVps:/home/user/file ~/Downloads`  will also work
