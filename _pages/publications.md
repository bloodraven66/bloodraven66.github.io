---
layout: page
permalink: /publications/
title: publications
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

<style>
  .pub-filter-btn {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.35rem 0.85rem;
    font-size: 0.82rem;
    font-weight: 500;
    border-radius: 20px;
    border: 1.5px solid var(--global-theme-color, #4285F4);
    color: var(--global-theme-color, #4285F4);
    background: transparent;
    cursor: pointer;
    white-space: nowrap;
    transition: background 0.15s, color 0.15s;
  }
  .pub-filter-btn:hover {
    background: var(--global-theme-color, #4285F4);
    color: #fff;
  }
  .pub-filter-dropdown {
    display: none;
    position: absolute;
    right: 0;
    top: calc(100% + 0.5rem);
    z-index: 100;
    background: var(--global-bg-color, #fff);
    border: 1px solid rgba(0,0,0,0.1);
    border-radius: 10px;
    padding: 1rem;
    box-shadow: 0 8px 24px rgba(0,0,0,0.12);
  }
  .pub-filter-dropdown .filter-actions {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 0.75rem;
    padding-bottom: 0.75rem;
    border-bottom: 1px solid rgba(0,0,0,0.08);
  }
  .pub-filter-dropdown .filter-actions button {
    flex: 1;
    padding: 0.25rem 0.5rem;
    font-size: 0.75rem;
    font-weight: 500;
    border-radius: 6px;
    border: none;
    cursor: pointer;
    transition: opacity 0.15s;
  }
  .pub-filter-dropdown .filter-actions button:hover { opacity: 0.85; }
  .pub-filter-dropdown .btn-select-all { background: #e8f5e9; color: #2e7d32; }
  .pub-filter-dropdown .btn-remove-all { background: #fce4ec; color: #c62828; }
  .pub-filter-dropdown .form-check {
    margin: 0;
    padding: 0;
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }
  .pub-filter-dropdown .form-check-input {
    cursor: pointer;
    flex-shrink: 0;
    margin: 0;
    position: static;
    float: none;
  }
  .pub-filter-dropdown .form-check-label {
    font-size: 0.82rem;
    cursor: pointer;
    user-select: none;
    white-space: nowrap;
    margin: 0;
    padding: 0;
  }
</style>

<!-- Bibsearch Feature -->
<div class="filter-container" style="display: flex; gap: 1.5rem; align-items: flex-start; margin-bottom: 2rem;">
  <div style="flex: 1;">
    {% include bib_search.liquid %}
  </div>

  <div class="keyword-filters" style="flex: 0 0 auto; position: relative;">
    <button id="toggle-keyword-filters" class="pub-filter-btn">
      🏷 Keyword ▾
    </button>
    <div id="keyword-filter-checkboxes" class="pub-filter-dropdown" style="min-width: 480px; right: auto; left: 0;">
      <div class="filter-actions">
        <button id="select-all-keywords" class="btn-select-all">✓ Select All</button>
        <button id="deselect-all-keywords" class="btn-remove-all">✕ Remove All</button>
      </div>
      <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 0.4rem 1.5rem;">
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="spoken dialogue system" id="filter-dialogue" checked>
          <label class="form-check-label" for="filter-dialogue">Spoken Dialogue</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="audio understanding" id="filter-audio" checked>
          <label class="form-check-label" for="filter-audio">Audio Understanding</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="evaluation" id="filter-eval" checked>
          <label class="form-check-label" for="filter-eval">Evaluation</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="dataset" id="filter-dataset" checked>
          <label class="form-check-label" for="filter-dataset">Dataset</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="speech recognition" id="filter-asr" checked>
          <label class="form-check-label" for="filter-asr">Speech Recognition</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="speech quality estimation" id="filter-sqe" checked>
          <label class="form-check-label" for="filter-sqe">Speech Quality</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="speech synthesis" id="filter-tts" checked>
          <label class="form-check-label" for="filter-tts">Speech Synthesis</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="neuroscience" id="filter-neuro" checked>
          <label class="form-check-label" for="filter-neuro">Neuroscience</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="speech production" id="filter-production" checked>
          <label class="form-check-label" for="filter-production">Speech Production</label>
        </div>
        <div class="form-check">
          <input class="form-check-input keyword-filter" type="checkbox" value="speech and health" id="filter-health" checked>
          <label class="form-check-label" for="filter-health">Speech and Health</label>
        </div>
      </div>
    </div>
  </div>

  <div class="conference-filters" style="flex: 0 0 auto; position: relative;">
    <button id="toggle-filters" class="pub-filter-btn">
      🎓 Conference ▾
    </button>
    <div id="filter-checkboxes" class="pub-filter-dropdown" style="min-width: 300px;">
      <div class="filter-actions">
        <button id="select-all" class="btn-select-all">✓ Select All</button>
        <button id="deselect-all" class="btn-remove-all">✕ Remove All</button>
      </div>
      <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 0.4rem 1.5rem;">
        <div class="form-check">
          <input class="form-check-input conference-filter" type="checkbox" value="ASRU" id="filter-asru" checked>
          <label class="form-check-label" for="filter-asru">ASRU</label>
        </div>
        <div class="form-check">
          <input class="form-check-input conference-filter" type="checkbox" value="AAAI" id="filter-aaai" checked>
          <label class="form-check-label" for="filter-aaai">AAAI</label>
        </div>
        <div class="form-check">
          <input class="form-check-input conference-filter" type="checkbox" value="ICASSP" id="filter-icassp" checked>
          <label class="form-check-label" for="filter-icassp">ICASSP</label>
        </div>
        <div class="form-check">
          <input class="form-check-input conference-filter" type="checkbox" value="NeurIPS" id="filter-neurips" checked>
          <label class="form-check-label" for="filter-neurips">NeurIPS</label>
        </div>
        <div class="form-check">
          <input class="form-check-input conference-filter" type="checkbox" value="Interspeech" id="filter-interspeech" checked>
          <label class="form-check-label" for="filter-interspeech">Interspeech</label>
        </div>
        <div class="form-check">
          <input class="form-check-input conference-filter" type="checkbox" value="IEEE Open Journal of Signal Processing" id="filter-ojsp" checked>
          <label class="form-check-label" for="filter-ojsp">IEEE OJSP</label>
        </div>
        <div class="form-check">
          <input class="form-check-input conference-filter" type="checkbox" value="The Journal of Physiology" id="filter-physiology" checked>
          <label class="form-check-label" for="filter-physiology">J. Physiology</label>
        </div>
        <div class="form-check">
          <input class="form-check-input conference-filter" type="checkbox" value="Under" id="filter-preprint" checked>
          <label class="form-check-label" for="filter-preprint">Preprints</label>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="publications">
{% bibliography %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const toggleBtn = document.getElementById('toggle-filters');
  const filterCheckboxes = document.getElementById('filter-checkboxes');
  const checkboxes = document.querySelectorAll('.conference-filter');
  const publications = document.querySelectorAll('.publications .bibliography li');
  const selectAllBtn = document.getElementById('select-all');
  const deselectAllBtn = document.getElementById('deselect-all');
  
  const toggleKeywordBtn = document.getElementById('toggle-keyword-filters');
  const keywordFilterCheckboxes = document.getElementById('keyword-filter-checkboxes');
  const keywordCheckboxes = document.querySelectorAll('.keyword-filter');
  const selectAllKeywordsBtn = document.getElementById('select-all-keywords');
  const deselectAllKeywordsBtn = document.getElementById('deselect-all-keywords');
  
  // Toggle conference filter visibility
  toggleBtn.addEventListener('click', function(e) {
    e.stopPropagation();
    const isHidden = filterCheckboxes.style.display !== 'block';
    keywordFilterCheckboxes.style.display = 'none';
    filterCheckboxes.style.display = isHidden ? 'block' : 'none';
  });
  
  // Toggle keyword filter visibility
  toggleKeywordBtn.addEventListener('click', function(e) {
    e.stopPropagation();
    const isHidden = keywordFilterCheckboxes.style.display !== 'block';
    filterCheckboxes.style.display = 'none';
    keywordFilterCheckboxes.style.display = isHidden ? 'block' : 'none';
  });

  // Prevent clicks inside dropdowns from closing them
  filterCheckboxes.addEventListener('click', function(e) { e.stopPropagation(); });
  keywordFilterCheckboxes.addEventListener('click', function(e) { e.stopPropagation(); });

  // Close dropdowns when clicking outside
  document.addEventListener('click', function() {
    filterCheckboxes.style.display = 'none';
    keywordFilterCheckboxes.style.display = 'none';
  });
  
  // Select all conferences
  selectAllBtn.addEventListener('click', function() {
    checkboxes.forEach(cb => cb.checked = true);
    filterPublications();
  });
  
  // Deselect all conferences
  deselectAllBtn.addEventListener('click', function() {
    checkboxes.forEach(cb => cb.checked = false);
    filterPublications();
  });
  
  // Select all keywords
  selectAllKeywordsBtn.addEventListener('click', function() {
    keywordCheckboxes.forEach(cb => cb.checked = true);
    filterPublications();
  });
  
  // Deselect all keywords
  deselectAllKeywordsBtn.addEventListener('click', function() {
    keywordCheckboxes.forEach(cb => cb.checked = false);
    filterPublications();
  });
  
  // Filter publications on change
  checkboxes.forEach(checkbox => {
    checkbox.addEventListener('change', filterPublications);
  });
  
  keywordCheckboxes.forEach(checkbox => {
    checkbox.addEventListener('change', filterPublications);
  });
  
  function filterPublications() {
    const selectedConferences = Array.from(checkboxes)
      .filter(cb => cb.checked)
      .map(cb => cb.value.toLowerCase());
    
    const selectedKeywords = Array.from(keywordCheckboxes)
      .filter(cb => cb.checked)
      .map(cb => cb.value.toLowerCase());
    
    publications.forEach(pub => {
      const row = pub.querySelector('.row[data-keywords]');
      const journalText = (row ? row.dataset.journal || '' : '').toLowerCase().trim();
      const pubKeywords = row
        ? row.dataset.keywords.split(',').map(k => k.trim().toLowerCase()).filter(k => k.length > 0)
        : [];

      // Check conference filter — hide if none selected
      let showByConference;
      if (selectedConferences.length === 0) {
        showByConference = false;
      } else {
        showByConference = selectedConferences.some(conf => journalText.includes(conf));
      }

      // Check keyword filter — hide if none selected
      let showByKeyword;
      if (selectedKeywords.length === 0) {
        showByKeyword = false;
      } else if (pubKeywords.length === 0) {
        showByKeyword = true;
      } else {
        showByKeyword = selectedKeywords.some(kw => pubKeywords.includes(kw));
      }
      
      pub.style.display = (showByConference && showByKeyword) ? '' : 'none';
    });
  }
});
</script>
