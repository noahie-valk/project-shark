This is the homepage. I am hoping to include the following sections:

- Concepts
- Projects
- Tools
- Playbooks

## Latest Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}
    </li>
  {% endfor %}
</ul>
