---
layout: default
title: About Me
---
I'm a senior software develper, I've specialized in web development, mainly in
desigining APIs using rails, I've worked in relatively high traffice websites
and I've tackled the problems that may appear due to scalability.

Also I have some interest in DevOps, I know how to set up deployments either by
using simple scripts like capistrano, or more complex stuff like AWS, I have
some experience using docker containers and chef for provisioninig machines.

I have some experience with html, css, js, but I don't like being a fullstack
developer, also I don't have any interest in mobile development.

Here's a simple table for a list of my skills that I use regularly

|Backend|
|:-
|Ruby on rails|Rspec|MySQL|Redis|
{: .no-border }

|Frontend|
|:-
|HTML|CSS|JS|
{: .no-border }

|DevOps|
|:-
|Chef|Docker|
{: .no-border }

|AWS|
|:-
|EC2|RDS|EB|OpsWorks
|S3|ElasticCache|
{: .no-border }

|Payments|
|:-
|Stripe|
{: .no-border }

|Source Control|
|:-
|GIT|
{: .no-border }

Here's some of my online profiles, which you can also find in the side bar on
the left

<p style='text-align: center'>
  {% for link in site.about_me_footer_links %}
    <td>
      <a href='{{ link.url }}' rel='nofollow' target='_blank'>
        | <i class='{{link.icon}}' ></i> {{link.name}} |
      </a>
    </td>
  {% endfor %}
</p>
