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
  data-name="{{ member.name | escape }}"
  data-info="{{ member.info | escape }}"
  data-bio="{{ member.bio | escape }}"
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

<script>
(function() {
  // Inject drawer into body once
  if (document.getElementById('member-drawer')) return;

  document.body.insertAdjacentHTML('beforeend', `
    <div id="drawer-overlay" onclick="closeDrawer()" style="position:fixed; inset:0; background:rgba(0,0,0,0.45); z-index:1000; opacity:0; transition:opacity 0.3s ease; pointer-events:none;"></div>
    <div id="member-drawer" style="position:fixed; top:0; right:0; height:100%; width:400px; max-width:92vw; background:var(--bg-card); z-index:1001; overflow-y:auto; box-shadow:-6px 0 32px rgba(0,0,0,0.18); border-left:1px solid var(--border-color); transform:translateX(100%); transition:transform 0.3s cubic-bezier(0.22,1,0.36,1);">
      <div style="display:flex; justify-content:flex-end; padding:1rem 1.25rem 0;">
        <button onclick="closeDrawer()" style="background:none; border:none; cursor:pointer; color:var(--text-secondary); font-size:1.4rem;">&times;</button>
      </div>
      <div style="text-align:center; padding:0.5rem 2rem 1.5rem;">
        <img id="drawer-photo" src="" alt="" style="width:130px; height:130px; object-fit:cover; border-radius:50%; border:3px solid var(--border-color); margin-bottom:1rem;">
        <h3 id="drawer-name" style="margin:0 0 0.25rem;"></h3>
        <p id="drawer-info" style="color:var(--accent); font-style:italic; font-size:0.9rem; margin:0;"></p>
      </div>
      <hr style="border:none; border-top:1px solid var(--border-color); margin:0 2rem 1.5rem;">
      <div style="padding:0 2rem 2rem;">
        <p id="drawer-bio" style="line-height:1.8; color:var(--text-primary); font-size:0.95rem; margin:0;"></p>
      </div>
    </div>
  `);

function openDrawer(card) {
  document.getElementById('drawer-name').textContent = card.dataset.name;
  document.getElementById('drawer-info').textContent = card.dataset.info;
  document.getElementById('drawer-bio').textContent  = card.dataset.bio;
  document.getElementById('drawer-photo').src        = card.dataset.photo;
  document.getElementById('drawer-photo').alt        = card.dataset.name;

  var drawer  = document.getElementById('member-drawer');
  var overlay = document.getElementById('drawer-overlay');

  overlay.style.pointerEvents = 'auto';
  overlay.style.opacity       = '1';
  drawer.style.transform      = 'translateX(0)';
  document.body.style.overflow = 'hidden';
}

function closeDrawer() {
  var drawer  = document.getElementById('member-drawer');
  var overlay = document.getElementById('drawer-overlay');

  drawer.style.transform      = 'translateX(100%)';
  overlay.style.opacity       = '0';
  overlay.style.pointerEvents = 'none';
  document.body.style.overflow = '';
}

  window.openDrawer  = openDrawer;
  window.closeDrawer = closeDrawer;

  document.addEventListener('keydown', function(e) {
    if (e.key === 'Escape') closeDrawer();
  });
})();
</script>
