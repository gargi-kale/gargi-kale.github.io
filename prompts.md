---
layout: page
title: Prompts
permalink: /prompts/
---

{% assign a = site.data.prompt_analysis %}

What does a month of asking an AI assistant actually look like? I exported my
Claude conversation history and ran a small NLP pipeline over **just my own
prompts** — cleaning the text, dropping stopwords and code, then pulling out the
words, phrases, and themes I kept coming back to. Everything below is
aggregated: word counts, themes, and daily activity, never the raw prompts
themselves.

<div class="stat-grid">
  <div class="stat-card"><span class="stat-num">{{ a.stats.conversations }}</span><span class="stat-label">conversations</span></div>
  <div class="stat-card"><span class="stat-num">{{ a.stats.prompts }}</span><span class="stat-label">prompts</span></div>
  <div class="stat-card"><span class="stat-num">{{ a.stats.words }}</span><span class="stat-label">words written</span></div>
  <div class="stat-card"><span class="stat-num">{{ a.stats.avg_words_per_prompt }}</span><span class="stat-label">avg words / prompt</span></div>
  <div class="stat-card"><span class="stat-num">{{ a.stats.unique_terms }}</span><span class="stat-label">unique terms</span></div>
</div>
<p class="muted">Spanning {{ a.stats.date_range }}.</p>

## What I talked about most

{% assign maxw = a.cloud[0].weight %}
<div class="word-cloud">
{% for w in a.cloud %}
  {% assign frac = w.weight | times: 100 | divided_by: maxw %}
  {% assign px = frac | times: 26 | divided_by: 100 | plus: 13 %}
  {% if frac > 66 %}{% assign tier = "wc-hi" %}{% elsif frac > 30 %}{% assign tier = "wc-mid" %}{% else %}{% assign tier = "wc-lo" %}{% endif %}
  <span class="{{ tier }}" style="font-size: {{ px }}px" title="{{ w.weight }} occurrences">{{ w.text }}</span>
{% endfor %}
</div>

## Themes

The same prompts, sorted into the areas I work in. Each share is the portion of
topic-bearing words that fell into that theme.

<div class="theme-list">
{% for t in a.themes %}
  <div class="theme-row">
    <div class="theme-head">
      <span class="theme-name">{{ t.label }}</span>
      <span class="theme-share">{{ t.share }}%</span>
    </div>
    <div class="theme-bar"><span style="width: {{ t.share }}%"></span></div>
    <p class="theme-terms">{% for term in t.terms %}<span class="tag">{{ term }}</span>{% endfor %}</p>
  </div>
{% endfor %}
</div>

## Recurring phrases

The two-word combinations that showed up most — a quick fingerprint of the
specific things I was digging into (word-embedding bias tests, GloVe vectors,
data pipelines).

<p class="phrase-list">
{% for b in a.bigrams %}<span class="tag">{{ b.text }}</span>{% endfor %}
</p>

## Daily activity

Prompts per day across the window.

{% assign maxd = 0 %}
{% for d in a.trend %}{% if d.prompts > maxd %}{% assign maxd = d.prompts %}{% endif %}{% endfor %}
<div class="trend-chart">
{% for d in a.trend %}
  {% assign h = d.prompts | times: 100 | divided_by: maxd %}
  <div class="trend-col" title="{{ d.label }}: {{ d.prompts }} prompts">
    <div class="trend-bar" style="height: {{ h }}%"></div>
    {% assign mod = forloop.index0 | modulo: 3 %}
    <span class="trend-label">{% if mod == 0 %}{{ d.label }}{% endif %}</span>
  </div>
{% endfor %}
</div>

<p class="muted">Generated from a personal Claude export with a Python +
scikit-learn pipeline (TF-IDF, frequency analysis, curated theme matching).
Last run {{ a.generated_at }}.</p>
