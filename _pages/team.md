---
title: "Team"
layout: gridlay
sitemap: false
permalink: /team/
---

## Team

**We are looking for new team members!**

## PI

<div class="section-card">
<div class="pi-card">
<img src="{{ site.url }}{{ site.baseurl }}/images/{{ site.photo }}" class="pi-photo" alt="{{ site.name }}" loading="lazy">
<div>
<h3 class="pi-name">{{ site.name }}</h3>
<p style="font-style: italic; color: var(--text-secondary);">{{ site.title }}, {{ site.institution }}</p>
<div class="pi-links">
{% if site.email %}<a href="mailto:{{ site.email }}" class="icon-link" title="Email"><i class="fa-solid fa-envelope"></i></a>{% endif %}
{% if site.links.google_scholar and site.links.google_scholar != "" %}<a href="{{ site.links.google_scholar }}" class="icon-link" title="Google Scholar"><i class="ai ai-google-scholar"></i></a>{% endif %}
{% if site.links.cv and site.links.cv != "" %}<a href="{{ site.url }}{{ site.baseurl }}/{{ site.links.cv }}" class="icon-link" title="CV"><i class="ai ai-cv"></i></a>{% endif %}
{% if site.links.github and site.links.github != "" %}<a href="{{ site.links.github }}" class="icon-link" title="GitHub"><i class="fa-brands fa-github"></i></a>{% endif %}
{% if site.links.researchgate and site.links.researchgate != "" %}<a href="{{ site.links.researchgate }}" class="icon-link" title="ResearchGate"><i class="ai ai-researchgate"></i></a>{% endif %}
</div>
{% if site.data.pi[0].education %}
<ul style="margin-top: var(--space-4);">
{% for education in site.data.pi[0].education %}
<li>{{ education | replace: "-","&#8211;" }}</li>
{% endfor %}
</ul>
{% endif %}
</div>
</div>
</div>

{% if site.data.team_members.size > 0 %}
## Current Students and Postdocs

<div class="team-grid">
{% for member in site.data.team_members %}
<div class="team-card"
  {% if member.bio %}onclick="openDrawer(this)" style="cursor: pointer;"{% endif %}
  data-name="{{ member.name }}"
  data-info="{{ member.info }}"
  data-bio="{{ member.bio }}"
  data-photo="{{ site.url }}{{ site.baseurl }}/images/{{ member.photo }}">
  <img src="{{ site.url }}{{ site.baseurl }}/images/{{ member.photo }}" class="team-photo" alt="{{ member.name }}" loading="lazy">
  <h4 class="team-name">{{ member.name }}</h4>
  <p class="team-info">{{ member.info }}</p>
  <div class="team-links">
    {% if member.email %}<a href="mailto:{{ member.email }}" class="icon-link" title="Email" onclick="event.stopPropagation()"><i class="fa-solid fa-envelope"></i></a>{% endif %}
    {% if member.website %}<a href="{{ member.website }}" class="icon-link" title="Website" onclick="event.stopPropagation()"><i class="fa-solid fa-house"></i></a>{% endif %}
    {% if member.scholar %}<a href="{{ member.scholar }}" class="icon-link" title="Google Scholar" onclick="event.stopPropagation()"><i class="ai ai-google-scholar"></i></a>{% endif %}
    {% if member.github %}<a href="{{ member.github }}" class="icon-link" title="GitHub" onclick="event.stopPropagation()"><i class="fa-brands fa-github"></i></a>{% endif %}
  </div>
  {% if member.bio %}<p style="font-size:0.78rem; color:var(--accent); margin-top:var(--space-2); margin-bottom:0;">Read more →</p>{% endif %}
</div>
{% endfor %}
</div>
{% endif %}

{% if site.data.alumni.size > 0 %}
## Alumni

<div class="section-card">
<table class="alumni-table">
<thead>
<tr><th>Name</th><th>Duration</th><th>Current Position</th></tr>
</thead>
<tbody>
{% for member in site.data.alumni %}
<tr>
<td>{{ member.name }}</td>
<td>{{ member.duration }}</td>
<td>{{ member.info }}</td>
</tr>
{% endfor %}
</tbody>
</table>
</div>
{% endif %}

## Administrative Support

<a href="mailto:exampleemail@gmail.com">Example staff</a> is helping us (and other groups) with administration.

<!-- Overlay -->
<div id="drawer-overlay" onclick="closeDrawer()" style="display:none; position:fixed; inset:0; background:rgba(0,0,0,0.45); z-index:1000; transition: opacity 0.25s ease;"></div>

<!-- Side Drawer -->
<div id="member-drawer" style="display:none; position:fixed; top:0; right:0; height:100%; width:400px; max-width:92vw; background:var(--bg-card); z-index:1001; overflow-y:auto; box-shadow:-6px 0 32px rgba(0,0,0,0.18); border-left: 1px solid var(--border-color);">
  
  <!-- Header bar -->
  <div style="display:flex; justify-content:flex-end; padding:1rem 1.25rem 0;">
    <button onclick="closeDrawer()" title="Close" style="background:none; border:none; cursor:pointer; color:var(--text-secondary); font-size:1.4rem; line-height:1; padding:0.25rem 0.5rem; border-radius:var(--radius-sm);">&times;</button>
  </div>

  <!-- Photo -->
  <div style="text-align:center; padding: 0.5rem 2rem 1.5rem;">
    <img id="drawer-photo" src="" alt="" style="width:130px; height:130px; object-fit:cover; border-radius:50%; border: 3px solid var(--border-color); margin-bottom:1rem;">
    <h3 id="drawer-name" style="margin:0 0 0.25rem;"></h3>
    <p id="drawer-info" style="color:var(--accent); font-style:italic; font-size:0.9rem; margin:0;"></p>
  </div>

  <!-- Divider -->
  <hr style="border:none; border-top:1px solid var(--border-color); margin: 0 2rem 1.5rem;">

  <!-- Bio -->
  <div style="padding: 0 2rem 2rem;">
    <p id="drawer-bio" style="line-height:1.8; color:var(--text-primary); font-size:0.95rem; margin:0;"></p>
  </div>

</div>

<script>
function openDrawer(card) {
  document.getElementById('drawer-name').textContent  = card.dataset.name;
  document.getElementById('drawer-info').textContent  = card.dataset.info;
  document.getElementById('drawer-bio').textContent   = card.dataset.bio;
  document.getElementById('drawer-photo').src         = card.dataset.photo;
  document.getElementById('drawer-photo').alt         = card.dataset.name;
  document.getElementById('member-drawer').style.display = 'block';
  document.getElementById('drawer-overlay').style.display = 'block';
  document.body.style.overflow = 'hidden';
}

function closeDrawer() {
  document.getElementById('member-drawer').style.display = 'none';
  document.getElementById('drawer-overlay').style.display = 'none';
  document.body.style.overflow = '';
}

document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') closeDrawer();
});
</script>
