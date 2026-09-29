---
layout: page
permalink: /publications/
title: publications
nav: true
nav_order: 1
---

<div class="publications">

<h2 class="bibliography">working papers</h2>
{% bibliography --group_by none --query @unpublished %}

<h2 class="bibliography">journal publications</h2>
{% bibliography --group_by none --query @article %}

<h2 class="bibliography">conference publications</h2>
{% bibliography --group_by none --query @inproceedings[keywords!=other] %}

<h2 class="bibliography">theses</h2>
{% bibliography --group_by none --query @phdthesis, @mastersthesis %}

<h2 class="bibliography">other</h2>
{% bibliography --group_by none --query @*[keywords=other] %}

</div>
