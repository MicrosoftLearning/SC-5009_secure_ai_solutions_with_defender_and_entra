---
title: Exercise Instructions
permalink: index.html
layout: home
---

<!--
Change the title above AND IN THE _config.yml FILE (so that the page header in the GitHub Pages site automatically shows the site name).

When you're ready for the labs to be live - make the repo public and enable GitHub Pages publishing from the main branch (in the repo Settings | Pages).
-->

This page lists exercises associated with Microsoft skilling content on [Microsoft Learn](https://learn.microsoft.com)

<!-- You can edit the paragraph above to provide a more specific description and links to content on Learn.

Include the following note if an Azure subscription is required (or add something similar for any other requirements, such as a Microsoft 365 account).

> **Note**: To complete these exercises, you will need a [Microsoft Azure subscription](https://azure.microsoft.com/free) in which you have sufficient permissions to create and configure the required resources.

If a more complex setup is required, create a separate markdown file with setup instructions at \Instructions\Labs\00-setup.md - being sure to include "lab.title"" metadata at the top so it shows up the list below
-->

<hr>

<!--- old page view
{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
{% for activity in labs  %}
{% if activity.lab.title %}
### [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }})


{% if activity.lab.level %}**Level**: {{activity.lab.level}} \| {% endif %}{% if activity.lab.duration %}**Duration**: {{activity.lab.duration}}{% endif %}

{% if activity.lab.description %}
*{{activity.lab.description}}*
{% endif %}
<hr>
{% endif %}
{% endfor %}
-->

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}

## Labs

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}

| Module | Exercise | Level | Duration |
| --- | --- | --- | --- |
{% for activity in labs %}{% if activity.lab.title %}| {{ activity.lab.module | default: " " }} | [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) | {{ activity.lab.level | default: " " }} | {{ activity.lab.duration | default: " " }} |
{% endif %}{% endfor %}

## Exercise summaries

<ul style="list-style-type: disc; padding-left: 20px;">
{% for activity in labs %}
{% if activity.lab.title and activity.lab.description %}
  <li style="margin-bottom: 16px;">
    <span style="font-weight: 600;">{{ activity.lab.title }}</span>
    <div style="margin-top: 4px;">{{ activity.lab.description }}</div>
  </li>
{% endif %}
{% endfor %}
</ul>

## table test

| Module | Exercise | Duration | Description |
| --- | --- | --- | --- |
{% for activity in labs %}{% if activity.lab.title %}| {{ activity.lab.module | default: " " }} | [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) | {{ activity.lab.duration | default: " " }} | {{ activity.lab.description | replace: "|", "&#124;" | default: " " }} |
{% endif %}{% endfor %}
