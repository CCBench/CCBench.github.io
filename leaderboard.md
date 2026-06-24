---
layout: page
title: Leaderboard
permalink: /leaderboard/
---

# Leaderboard

Benchmark results for communication and compression performance across different backends and configurations.

<div class="table-controls">
  <label for="backend-filter">Backend:</label>
  <select id="backend-filter" onchange="filterTable()">
    <option value="all">All</option>
    <option value="MPI">MPI</option>
    <option value="NCCL">NCCL</option>
    <option value="RCCL">RCCL</option>
  </select>

  <label for="metric-filter" style="margin-left: 1rem;">Metric:</label>
  <select id="metric-filter" onchange="filterTable()">
    <option value="all">All</option>
    <option value="Bandwidth">Bandwidth</option>
    <option value="Latency">Latency</option>
    <option value="Throughput">Throughput</option>
  </select>
</div>

<table id="leaderboard-table" class="leaderboard">
  <thead>
    <tr>
      <th onclick="sortTable(0)">Rank</th>
      <th onclick="sortTable(1)">Model / Config</th>
      <th onclick="sortTable(2)">Backend</th>
      <th onclick="sortTable(3)">Metric</th>
      <th onclick="sortTable(4)">Value</th>
      <th onclick="sortTable(5)">Date</th>
    </tr>
  </thead>
  <tbody>
    {% assign sorted = site.data.leaderboard | sort: "value" | reverse %}
    {% for entry in sorted %}
    <tr data-backend="{{ entry.backend }}" data-metric="{{ entry.metric }}">
      <td>{{ forloop.index }}</td>
      <td>{{ entry.model }}</td>
      <td>{{ entry.backend }}</td>
      <td>{{ entry.metric }}</td>
      <td>{{ entry.value }} {{ entry.unit }}</td>
      <td>{{ entry.date }}</td>
    </tr>
    {% endfor %}
  </tbody>
</table>

<script>
function filterTable() {
  var backend = document.getElementById('backend-filter').value;
  var metric = document.getElementById('metric-filter').value;
  var rows = document.querySelectorAll('#leaderboard-table tbody tr');
  rows.forEach(function(row) {
    var showBackend = backend === 'all' || row.dataset.backend === backend;
    var showMetric = metric === 'all' || row.dataset.metric === metric;
    row.style.display = showBackend && showMetric ? '' : 'none';
  });
}

function sortTable(col) {
  var table = document.getElementById('leaderboard-table');
  var tbody = table.querySelector('tbody');
  var rows = Array.from(tbody.querySelectorAll('tr'));
  var dir = table.dataset.sortDir === 'asc' ? 'desc' : 'asc';
  table.dataset.sortDir = dir;

  rows.sort(function(a, b) {
    var aVal = a.children[col].textContent.trim();
    var bVal = b.children[col].textContent.trim();
    var aNum = parseFloat(aVal), bNum = parseFloat(bVal);
    if (!isNaN(aNum) && !isNaN(bNum)) {
      return dir === 'asc' ? aNum - bNum : bNum - aNum;
    }
    return dir === 'asc' ? aVal.localeCompare(bVal) : bVal.localeCompare(aVal);
  });

  rows.forEach(function(row, i) {
    row.children[0].textContent = i + 1;
    tbody.appendChild(row);
  });
}
</script>
