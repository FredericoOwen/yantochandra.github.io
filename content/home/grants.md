---
widget: blank
headless: true
weight: 30
active: true
title: Grants and Awards
---

## Grants and Awards

{{< awards_list sort="desc" >}}

<div class="awards-controls mt-4 mb-3">
  <small class="text-muted">Sort by date:</small>
  <button class="btn btn-sm btn-outline-secondary me-2" onclick="sortAwards('desc')">Newest First ↓</button>
  <button class="btn btn-sm btn-outline-secondary" onclick="sortAwards('asc')">Oldest First ↑</button>
</div>

<div id="awards-container">
  {{ range $index, $award := $.Site.Data.awards }}
  <div class="award-item mb-3" data-date="{{ $award.date }}">
    <div class="card h-100">
      <div class="card-body">
        <h5 class="card-title">
          <a href="{{ $award.link }}" target="_blank" rel="noopener" class="text-decoration-none">
            {{ $award.title }}
            <i class="fas fa-external-link-alt ms-1 small"></i>
          </a>
        </h5>
        <div class="d-flex flex-wrap gap-2 mb-2">
          <span class="badge bg-primary">{{ $award.date_display }}</span>
          {{ if $award.category }}
          <span class="badge bg-secondary">{{ $award.category }}</span>
          {{ end }}
          {{ if $award.amount }}
          <span class="badge bg-success">{{ $award.amount }}</span>
          {{ end }}
        </div>
        {{ if $award.description }}
        <p class="card-text small text-muted mb-0">{{ $award.description | markdownify }}</p>
        {{ end }}
      </div>
    </div>
  </div>
  {{ end }}
</div>

<!-- Sorting Script -->
<script>
function sortAwards(order) {
  const container = document.getElementById('awards-container');
  const awards = Array.from(container.querySelectorAll('.award-item'));
  
  awards.sort((a, b) => {
    const dateA = new Date(a.dataset.date);
    const dateB = new Date(b.dataset.date);
    return order === 'asc' ? dateA - dateB : dateB - dateA;
  });
  
  // Re-append in sorted order
  awards.forEach(award => container.appendChild(award));
}

// Initialize with default sort (descending)
document.addEventListener('DOMContentLoaded', () => {
  sortAwards('desc');
});
</script>

<!-- Custom CSS for Awards -->
<style>
.award-item .card {
  transition: transform 0.2s, box-shadow 0.2s;
  border-left: 4px solid #0d6efd;
}
.award-item .card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}
.award-item a {
  color: inherit;
}
.award-item a:hover {
  color: #0d6efd;
}
.awards-controls {
  text-align: right;
}
@media (max-width: 768px) {
  .awards-controls {
    text-align: left;
  }
}
</style>