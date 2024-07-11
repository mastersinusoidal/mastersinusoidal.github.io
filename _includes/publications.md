<h2 id="publications" style="margin: 2px 0px -15px;">Publications</h2>
<div class="publications">
<ol class="bibliography">

{% for link in site.data.publications.main %}

<li>
<div class="pub-row">

  <div class="col-sm-3 abbr" style="position: relative;padding-right: 15px;padding-left: 15px;">
    <img src="assets/img/teaser_example.png" class="teaser img-fluid z-depth-1">
    <abbr class="badge">CVPR</abbr>
    <img src="{{ link.image }}" class="teaser img-fluid z-depth-1" style="width=100;height=40%">
            <abbr class="badge">{{ link.conference_short }}</abbr>
  </div>

  <div class="col-sm-9" style="position: relative;padding-right: 15px;padding-left: 20px;">
    <div class="title"><a href="https://arxiv.org/pdf/2002.10211.pdf">Mnemonics Training: Multi-Class Incremental Learning without Forgetting</a></div>
    <div class="author"><strong>Yaoyao Liu</strong>, Yuting Su, An-An Liu, Bernt Schiele, Qianru Sun</div>
    <div class="periodical"><em>IEEE/CVF Conference on Computer Vision and Pattern Recognition <strong>(CVPR)</strong>, 2020.</em></div>
      <div class="title"><a href="{{ link.pdf }}">{{ link.title }}</a></div>
      <div class="author">{{ link.authors }}</div>
      <div class="periodical"><em>{{ link.conference }}</em>
      </div>
    <div class="links">
      <a href="https://arxiv.org/pdf/2002.10211.pdf" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">PDF</a>
      <a href="https://github.com/yaoyao-liu/mnemonics" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">Code</a>
      <a href="https://class-il.mpi-inf.mpg.de/mnemonics/" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">Project Page</a>
      <a href="https://dblp.uni-trier.de/rec/conf/cvpr/LiuSLSS20.html?view=bibtex" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">BibTex</a>
      <strong><i style="color:#e74d3c">Oral Presentation</i></strong>
      {% if link.pdf %} 
      <a href="{{ link.pdf }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">PDF</a>
      {% endif %}
      {% if link.code %} 
      <a href="{{ link.code }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">Code</a>
      {% endif %}
      {% if link.page %} 
      <a href="{{ link.page }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">Project Page</a>
      {% endif %}
      {% if link.bibtex %} 
      <a href="{{ link.bibtex }}" class="btn btn-sm z-depth-0" role="button" target="_blank" style="font-size:12px;">BibTex</a>
      {% endif %}
      {% if link.notes %} 
      <strong> <i style="color:#e74d3c">{{ link.notes }}</i></strong>
      {% endif %}
      {% if link.others %} 
      {{ link.others }}
      {% endif %}
    </div>
  </div>
</div>
</li>
  

<br>

{% endfor %}

</ol>
</div>
