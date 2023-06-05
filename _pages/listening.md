---
layout: default
title: Listening
description: What I've Been Listening To
subtitle: What I've Been Listening To Recently
featured_image: /images/social.jpg
---
<section class="single">

	<div class="wrap">

		<h1>{{ page.title }}</h1>
		{% for week in site.data.streaming %}
		<h3>Week of: {{ week.date | date: "%B %-d %Y" }}</h3>
		<table>
			<thead>
				<td>Album</td>
				<td>Artist</td>
			</thead>
			<tbody>
				{% for album in week.albums %}
				<tr>
					<td>{{album.title}}</td><td>{{ album.artist }}</td>
				</tr>			
				{% endfor %}
			</tbody>
		</table>
	  {% endfor %}
	</div>

</section>