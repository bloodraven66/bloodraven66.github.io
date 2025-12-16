---
layout: page
permalink: /publications/
title: publications
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->
<div class="filter-container" style="display: flex; gap: 2rem; align-items: flex-start; margin-bottom: 2rem;">
  <div style="flex: 1;">
    {% include bib_search.liquid %}
  </div>
  
  <div class="keyword-filters" style="flex: 0 0 auto;">
    <button id="toggle-keyword-filters" class="btn btn-sm btn-outline-primary" style="margin-bottom: 0.5rem;">
      Filter by Keyword ▼
    </button>
    <div id="keyword-filter-checkboxes" style="display: none;">
      <div style="display: flex; gap: 0.5rem; margin-bottom: 0.5rem;">
        <button id="select-all-keywords" class="btn btn-sm" style="font-size: 0.75rem; padding: 0.2rem 0.5rem; background-color: #28a745; color: white; border: none;">Select All</button>
        <button id="deselect-all-keywords" class="btn btn-sm" style="font-size: 0.75rem; padding: 0.2rem 0.5rem; background-color: #dc3545; color: white; border: none;">Remove All</button>
      </div>
      <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 0.5rem;">
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
  
  <div class="conference-filters" style="flex: 0 0 auto;">
    <button id="toggle-filters" class="btn btn-sm btn-outline-primary" style="margin-bottom: 0.5rem;">
      Filter by Conference ▼
    </button>
    <div id="filter-checkboxes" style="display: none;">
      <div style="display: flex; gap: 0.5rem; margin-bottom: 0.5rem;">
        <button id="select-all" class="btn btn-sm" style="font-size: 0.75rem; padding: 0.2rem 0.5rem; background-color: #28a745; color: white; border: none;">Select All</button>
        <button id="deselect-all" class="btn btn-sm" style="font-size: 0.75rem; padding: 0.2rem 0.5rem; background-color: #dc3545; color: white; border: none;">Remove All</button>
      </div>
      <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 0.5rem;">
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
          <input class="form-check-input conference-filter" type="checkbox" value="Under submission" id="filter-preprint" checked>
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
  toggleBtn.addEventListener('click', function() {
    const isHidden = filterCheckboxes.style.display === 'none';
    filterCheckboxes.style.display = isHidden ? 'block' : 'none';
    toggleBtn.textContent = isHidden ? 'Filter by Conference ▲' : 'Filter by Conference ▼';
  });
  
  // Toggle keyword filter visibility
  toggleKeywordBtn.addEventListener('click', function() {
    const isHidden = keywordFilterCheckboxes.style.display === 'none';
    keywordFilterCheckboxes.style.display = isHidden ? 'block' : 'none';
    toggleKeywordBtn.textContent = isHidden ? 'Filter by Keyword ▲' : 'Filter by Keyword ▼';
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
      const journal = pub.querySelector('.periodical');
      const keywordBadges = pub.querySelectorAll('.keywords .badge');
      
      let showByConference = false;
      let showByKeyword = false;
      
      // Check conference filter
      if (selectedConferences.length === 0) {
        showByConference = true; // Show all if no filter selected
      } else if (journal) {
        const journalText = journal.textContent.toLowerCase();
        showByConference = selectedConferences.some(conf => 
          journalText.includes(conf.toLowerCase())
        );
      }
      
      // Check keyword filter
      if (selectedKeywords.length === 0) {
        showByKeyword = true; // Show all if no filter selected
      } else if (keywordBadges.length === 0) {
        showByKeyword = true; // Show papers without keywords
      } else {
        const pubKeywords = Array.from(keywordBadges).map(badge => 
          badge.textContent.trim().toLowerCase()
        );
        showByKeyword = selectedKeywords.some(keyword => 
          pubKeywords.includes(keyword)
        );
      }
      
      // Show publication only if it matches both filters
      pub.style.display = (showByConference && showByKeyword) ? '' : 'none';
    });
  }
});
</script>
