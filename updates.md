---
layout: default
title: Updates
description: Subscribe to NEST updates and see what's changed.
---

# Updates

Subscribe to get an email when NEST changes — new Adomin features, stream setup
tweaks, and guide updates. Emails go out **only when there's something worth
sharing** — no fixed schedule, no spam.

<form
  action="https://buttondown.com/api/emails/embed-subscribe/enpicie"
  method="post"
  target="popupwindow"
  onsubmit="window.open('https://buttondown.com/enpicie', 'popupwindow')"
  class="not-prose flex flex-col sm:flex-row gap-2 my-6 max-w-md"
>
  <input
    type="email"
    name="email"
    required
    placeholder="you@example.com"
    aria-label="Email address"
    class="flex-1 px-4 py-2.5 rounded-lg bg-slate-900 border border-slate-700 text-slate-100 placeholder-slate-500 focus:outline-none focus:border-indigo-400 focus:ring-1 focus:ring-indigo-400 transition-colors"
  />
  <button
    type="submit"
    class="px-5 py-2.5 rounded-lg font-semibold text-white bg-gradient-to-r from-indigo-500 to-purple-500 hover:from-indigo-400 hover:to-purple-400 transition-colors cursor-pointer whitespace-nowrap"
  >
    Subscribe
  </button>
</form>

<p class="not-prose text-xs text-slate-500 mb-10">
  No spam. Unsubscribe anytime — every email has a one-click unsubscribe link.
  Updates also posted to X from <a href="https://twitter.com/enpicie" class="text-indigo-400 hover:text-indigo-300">@enpicie</a>.
</p>

---

## What's changed

<p class="not-prose text-sm mb-6">
  Recent updates are listed below. <a href="https://buttondown.com/enpicie/archive/" class="text-indigo-400 hover:text-indigo-300">Browse the full archive on Buttondown&nbsp;→</a>
</p>

<div class="not-prose flex flex-col gap-5 mt-6">
{% for update in site.data.updates %}
  <article class="bg-slate-900 border border-slate-800 rounded-xl p-5">
    <div class="flex items-baseline justify-between gap-3 flex-wrap mb-2">
      <h3 class="font-bold text-slate-100 text-base m-0">{{ update.title }}</h3>
      <time datetime="{{ update.date | date_to_xmlschema }}" class="text-xs text-slate-500 whitespace-nowrap">
        {{ update.date | date: "%b %-d, %Y" }}
      </time>
    </div>
    {% if update.tags %}
    <div class="flex flex-wrap gap-1.5 mb-3">
      {% for tag in update.tags %}
      <span class="px-2 py-0.5 rounded-md text-[10px] font-semibold uppercase tracking-wide text-indigo-300 bg-indigo-500/10 border border-indigo-500/20">{{ tag }}</span>
      {% endfor %}
    </div>
    {% endif %}
    <div class="text-sm text-slate-300 leading-relaxed">{{ update.body | markdownify }}</div>
  </article>
{% endfor %}
</div>
