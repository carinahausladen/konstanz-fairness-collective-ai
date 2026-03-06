---
layout: default
title: "Seminar Schedule"
---

<table class="schedule-table">
  <thead>
    <tr>
      <th>Week · Date</th>
      <th>Topic</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><span class="week">1</span> <span class="date">08 Apr</span></td><td><span class="topic">Introduction</span></td></tr>
    <tr class="schedule-row" data-href="{{ '/week-01/week-02/' | relative_url }}"><td><span class="week">2</span> <span class="date">15 Apr</span></td><td><span class="topic">Defining and Measuring Fairness in AI</span></td></tr>
    <tr class="schedule-row" data-href="{{ '/week-01/week-02/' | relative_url }}"><td><span class="week">3</span> <span class="date">22 Apr</span></td><td><span class="topic">Defining and Measuring Fairness in AI</span></td></tr>
    <tr class="schedule-row" data-href="{{ '/week-03/' | relative_url }}"><td><span class="week">4</span> <span class="date">29 Apr</span></td><td><span class="topic">Social Choice and AI Alignment</span></td></tr>
    <tr class="schedule-row" data-href="{{ '/week-03/' | relative_url }}"><td><span class="week">5</span> <span class="date">06 May</span></td><td><span class="topic">Social Choice and AI Alignment</span></td></tr>
    <tr class="schedule-row" data-href="{{ '/week-04/' | relative_url }}"><td><span class="week">6</span> <span class="date">13 May</span></td><td><span class="topic">Current Ethics Debates</span></td></tr>
    <tr class="schedule-row" data-href="{{ '/week-05/' | relative_url }}"><td><span class="week">7</span> <span class="date">20 May</span></td><td><span class="topic">Democracy and LLMs</span></td></tr>
  </tbody>
</table>

<script>
  document.querySelectorAll('.schedule-row[data-href]').forEach((row) => {
    const destination = row.dataset.href;
    row.classList.add('is-clickable');
    row.tabIndex = 0;
    row.setAttribute('role', 'button');

    row.addEventListener('click', () => {
      window.location.href = destination;
    });

    row.addEventListener('keydown', (event) => {
      if (event.key === 'Enter' || event.key === ' ') {
        event.preventDefault();
        window.location.href = destination;
      }
    });
  });
</script>
