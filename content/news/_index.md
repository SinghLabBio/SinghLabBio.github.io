---
title: News & updates
description: Latest updates from the Singh Lab
---

I know long term these news pages can deprecate, so I'm just going to embed
my bluesky feed below. 
Follow social media for the latest updates in my lab!

Sometimes I will try to blog about various thoughts I have in long-form (linked below)

{{< cards cols="2" >}}
{{< card link="https://www.linkedin.com/in/sukrit-singh-9797587b/" title="LinkedIn" subtitle="Connect with me on LinkedIn" icon="linkedin" >}}
{{< card link="https://x.com/sukritsingh92" title="X / Twitter" subtitle="@sukritsingh92" icon="x-twitter" >}}
{{< card link="https://bsky.app/profile/sukritsingh92.bsky.social"  title="BlueSky" subtitle="Follow me on BlueSky @sukritsingh92.bsky.social" icon="bluesky" >}}
{{< card link="https://sukritsingh.github.io/blog/" title="Blog" subtitle="Longer-form thoughts on various topics" icon="pencil" >}}
{{< /cards >}}

<!-- Embed bluesky feed below -->

<style>
  .sl-bsky { margin: 1.5rem 0; }
  .sl-bsky-head { display:flex; justify-content:space-between; align-items:baseline; gap:1rem; flex-wrap:wrap; margin-bottom:.6rem; font-size:1.5em; font-weight:600; }
  .sl-bsky-head a { font-weight:400; font-size:.9em; text-decoration:none; color:hsl(var(--primary-hue) var(--primary-saturation) var(--primary-lightness)); }
  .sl-bsky-head a:hover { text-decoration:underline; }
  .sl-bsky-box { max-height: 75vh; overflow-y:auto; padding:1rem; border:1px solid rgb(127 127 127 / .35); border-radius:.75rem; background:rgb(127 127 127 / .04); scrollbar-gutter:stable; }
  .dark .sl-bsky-box { background:#1f1f24; border-color:#34343d; }
  .sl-bsky-post { padding:1rem; margin-bottom:1rem; border:1px solid rgb(127 127 127 / .3); border-radius:.6rem; background:rgb(255 255 255 / .6); }
  .dark .sl-bsky-post { background:#232329; border-color:#34343d; }
  .sl-bsky-post:last-child { margin-bottom:0; }
  .sl-bsky-meta { display:flex; justify-content:space-between; gap:1rem; font-size:.8em; opacity:.7; margin-bottom:.4rem; }
  .sl-bsky-meta a { text-decoration:none; color:inherit; }
  .sl-bsky-meta a:hover { text-decoration:underline; }
  .sl-bsky-text { margin:0; white-space:pre-line; overflow-wrap:anywhere; line-height:1.5; font-size:1.2em; }
  .sl-bsky-text a { text-decoration:underline; color:hsl(var(--primary-hue) var(--primary-saturation) var(--primary-lightness)); }
  .sl-bsky-imgs { display:grid; gap:.4rem; margin-top:.6rem; grid-template-columns:repeat(auto-fit, minmax(160px, 1fr)); }
  .sl-bsky-imgs img { width:100%; max-height:420px; object-fit:contain; border-radius:.4rem; border:1px solid rgb(127 127 127 / .25); background:rgb(127 127 127 / .08); }
  .sl-bsky-card { display:block; margin-top:.6rem; padding:.6rem .8rem; border:1px solid rgb(127 127 127 / .3); border-radius:.5rem; text-decoration:none; color:inherit; font-size:.85em; }
  .sl-bsky-card:hover { background:rgb(127 127 127 / .08); }
  .sl-bsky-card strong { display:block; }
  .sl-bsky-card span { opacity:.75; }
  .sl-bsky-quote { margin-top:.6rem; padding:.5rem .8rem; border-left:3px solid rgb(127 127 127 / .4); font-size:.85em; opacity:.85; }
  .sl-bsky-status { padding:1rem; opacity:.75; }
</style>

<div id="sl-bsky" class="sl-bsky not-prose" data-handle="sukritsingh92.bsky.social" data-limit="10"></div>

<script>
(function () {
  var root   = document.getElementById('sl-bsky');
  var handle = root.dataset.handle;
  var limit  = parseInt(root.dataset.limit, 10) || 10;
  var profile = 'https://bsky.app/profile/' + handle;

  var esc = function (s) {
    return String(s == null ? '' : s).replace(/[&<>"']/g, function (c) {
      return { '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c];
    });
  };
  var enc = new TextEncoder(), dec = new TextDecoder();

  // Link/mention/hashtag positions are UTF-8 BYTE offsets, so slice bytes, not characters.
  function richText(text, facets) {
    var bytes = enc.encode(text || '');
    var list = (facets || []).slice().sort(function (a, b) { return a.index.byteStart - b.index.byteStart; });
    var out = '', pos = 0;
    list.forEach(function (f) {
      var s = f.index.byteStart, e = f.index.byteEnd;
      if (s < pos || e > bytes.length) return;
      out += esc(dec.decode(bytes.slice(pos, s)));
      var seg = esc(dec.decode(bytes.slice(s, e)));
      var href = null;
      (f.features || []).forEach(function (ft) {
        if (ft.$type === 'app.bsky.richtext.facet#link')    href = ft.uri;
        if (ft.$type === 'app.bsky.richtext.facet#mention') href = 'https://bsky.app/profile/' + ft.did;
        if (ft.$type === 'app.bsky.richtext.facet#tag')     href = 'https://bsky.app/hashtag/' + encodeURIComponent(ft.tag);
      });
      out += href ? '<a href="' + esc(href) + '" target="_blank" rel="noopener noreferrer">' + seg + '</a>' : seg;
      pos = e;
    });
    out += esc(dec.decode(bytes.slice(pos)));
    return out;
  }

  function images(imgs) {
    if (!imgs || !imgs.length) return '';
    return '<div class="sl-bsky-imgs">' + imgs.map(function (im) {
      return '<a href="' + esc(im.fullsize || im.thumb) + '" target="_blank" rel="noopener noreferrer">' +
             '<img src="' + esc(im.thumb) + '" alt="' + esc(im.alt) + '" loading="lazy"></a>';
    }).join('') + '</div>';
  }

  function embed(em, postUrl) {
    if (!em) return '';
    var t = em.$type || '';
    if (t.indexOf('embed.images') > -1)  return images(em.images);
    if (t.indexOf('embed.video') > -1)   return em.thumbnail
      ? '<div class="sl-bsky-imgs"><a href="' + esc(postUrl) + '" target="_blank" rel="noopener noreferrer"><img src="' + esc(em.thumbnail) + '" alt="' + esc(em.alt || 'Video, view on Bluesky') + '" loading="lazy"></a></div>' : '';
    if (t.indexOf('embed.external') > -1) {
      var x = em.external || {};
      return '<a class="sl-bsky-card" href="' + esc(x.uri) + '" target="_blank" rel="noopener noreferrer">' +
             '<strong>' + esc(x.title || x.uri) + '</strong><span>' + esc(x.description) + '</span></a>';
    }
    if (t.indexOf('embed.recordWithMedia') > -1) return embed(em.media, postUrl) + embed(em.record, postUrl);
    if (t.indexOf('embed.record') > -1) {
      var r = em.record || {};
      var a = r.author || {};
      var url = a.handle && r.uri ? 'https://bsky.app/profile/' + a.handle + '/post/' + r.uri.split('/').pop() : profile;
      var txt = (r.value && r.value.text) || '';
      return '<div class="sl-bsky-quote">Quoting <a href="' + esc(url) + '" target="_blank" rel="noopener noreferrer">@' + esc(a.handle || 'post') + '</a>' +
             (txt ? ': ' + esc(txt.length > 200 ? txt.slice(0, 200) + '…' : txt) : '') + '</div>';
    }
    return '';
  }

  function renderPost(post) {
    var url = 'https://bsky.app/profile/' + post.author.handle + '/post/' + post.uri.split('/').pop();
    var when = new Date(post.record.createdAt).toLocaleDateString(undefined, { year: 'numeric', month: 'long', day: 'numeric' });
    return '<article class="sl-bsky-post">' +
      '<div class="sl-bsky-meta"><time datetime="' + esc(post.record.createdAt) + '">' + esc(when) + '</time>' +
      '<a href="' + esc(url) + '" target="_blank" rel="noopener noreferrer">View on Bluesky &rarr;</a></div>' +
      '<p class="sl-bsky-text">' + richText(post.record.text, post.record.facets) + '</p>' +
      embed(post.embed, url) +
      '</article>';
  }

  root.innerHTML = '<div class="sl-bsky-head"><span>My BlueSky feed - embedded for convenience</span>' +
    '<a href="' + esc(profile) + '" target="_blank" rel="noopener noreferrer">Follow @' + esc(handle) + ' &rarr;</a></div>' +
    '<div class="sl-bsky-box"><div class="sl-bsky-status">Loading posts…</div></div>';
  var box = root.querySelector('.sl-bsky-box');

  var api = 'https://public.api.bsky.app/xrpc/app.bsky.feed.getAuthorFeed' +
            '?actor=' + encodeURIComponent(handle) +
            '&limit=' + Math.min(limit * 3, 100) +
            '&filter=posts_no_replies';   // change to posts_and_author_threads to include your own thread replies

  fetch(api).then(function (r) {
    if (!r.ok) throw new Error('HTTP ' + r.status);
    return r.json();
  }).then(function (data) {
    var mine = (data.feed || []).filter(function (item) {
      return !item.reason &&   // reposts carry a `reason`; drop them
             item.post && item.post.author && item.post.author.handle === handle;
    }).slice(0, limit);
    box.innerHTML = mine.length ? mine.map(function (i) { return renderPost(i.post); }).join('')
      : '<div class="sl-bsky-status">No posts yet. <a href="' + esc(profile) + '">Visit the profile &rarr;</a></div>';
  }).catch(function (err) {
    box.innerHTML = '<div class="sl-bsky-status">Could not load the live feed (' + esc(err.message) + '). ' +
      '<a href="' + esc(profile) + '" target="_blank" rel="noopener noreferrer">Read the latest posts on Bluesky &rarr;</a></div>';
  });
})();
</script>