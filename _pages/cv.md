---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

[Download my CV (PDF)]({{ base_path }}/files/XiaolongGuo.pdf)

*Last updated: <span id="cv-last-updated">…</span>*

<script>
fetch("{{ base_path }}/files/XiaolongGuo.pdf", { method: "HEAD" })
  .then(function (resp) {
    var lastModified = resp.headers.get("Last-Modified");
    if (lastModified) {
      var d = new Date(lastModified);
      document.getElementById("cv-last-updated").textContent =
        d.getFullYear() + "-" +
        String(d.getMonth() + 1).padStart(2, "0") + "-" +
        String(d.getDate()).padStart(2, "0");
    } else {
      document.getElementById("cv-last-updated").textContent = "unknown";
    }
  })
  .catch(function () {
    document.getElementById("cv-last-updated").textContent = "unknown";
  });
</script>
