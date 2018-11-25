---
permalink: /
---

![Schüler Roboter](images/rover.jpg)

* [Über das Projekt](project/)
* [News](news/)
  <ul>
    {% for post in site.posts %}
      <li>{{ post.date | date: "%d-%b-%Y" }} <a href="{{ post.url }}">{{ post.title }}</a></li>
      {% if forloop.index == 5 %}
        {% break %}
      {% endif %}
    {% endfor %}
  </ul>
* Anleitungen
  * [Bau des Roboters](tutorials/build_a_robot/)
  * [Basisinstallation Software](tutorials/software_image/)
  * [Programmieren mit Scratch](tutorials/programming_with_scratch/)
  * [Bilderkennung mit OpenCV](tutorials/image_recognition_with_opencv/)
* [Kontakt](contact/)
