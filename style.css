/* Student profile renderer — data comes from the Google Sheet (see config.js).
   If the sheet can't be reached, data.js (embedded copy) is used instead. */
(function () {
  var W = typeof window !== 'undefined' ? window : {};
  var AVATAR = 'data:image/svg+xml;utf8,' + encodeURIComponent(
    '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 120 120"><rect width="120" height="120" fill="#fffdf6"/>' +
    '<circle cx="60" cy="44" r="22" fill="#0c2c22"/><ellipse cx="60" cy="112" rx="42" ry="34" fill="#0c2c22"/></svg>');
  var SVG = {
    call: '<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M6.6 10.8c1.4 2.8 3.8 5.1 6.6 6.6l2.2-2.2c.3-.3.7-.4 1-.2 1.1.4 2.3.6 3.6.6.6 0 1 .4 1 1V20c0 .6-.4 1-1 1C10.5 21 3 13.5 3 4c0-.6.4-1 1-1h3.2c.6 0 1 .4 1 1 0 1.3.2 2.5.6 3.6.1.4 0 .8-.2 1L6.6 10.8z"/></svg>',
    wa: '<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2a10 10 0 0 0-8.6 15.1L2 22l5.1-1.3A10 10 0 1 0 12 2zm5.8 14.2c-.2.7-1.4 1.3-2 1.4-.5.1-1.2.1-1.9-.1-.4-.1-1-.3-1.7-.6-3-1.3-4.9-4.3-5-4.5-.1-.2-1.2-1.6-1.2-3 0-1.4.7-2.1 1-2.4.3-.3.6-.3.8-.3h.6c.2 0 .4 0 .6.5.2.5.8 1.9.8 2 .1.2.1.3 0 .5-.1.2-.2.3-.3.5-.2.2-.3.3-.5.5-.2.2-.3.4-.1.7.2.3.8 1.3 1.7 2.1 1.2 1 2.1 1.4 2.4 1.5.3.1.5.1.6-.1.2-.2.7-.8.9-1.1.2-.3.4-.2.6-.1.2.1 1.6.7 1.8.9.2.1.4.2.5.3.1.2.1.9-.1 1.6z"/></svg>',
    fb: '<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M13.5 21v-8h2.7l.4-3.1h-3.1V8c0-.9.2-1.5 1.6-1.5H17V3.6C16.7 3.5 15.6 3.4 14.4 3.4c-2.5 0-4.3 1.5-4.3 4.4v2.1H7.4V13H10v8h3.5z"/></svg>',
    mail: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="3" y="5" width="18" height="14" rx="2"/><path d="M3.5 7l8.5 6 8.5-6"/></svg>',
    lPhone: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 4h4l2 5-2.5 1.5a11 11 0 0 0 5 5L15 13l5 2v4a2 2 0 0 1-2 2A16 16 0 0 1 3 6a2 2 0 0 1 2-2z"/></svg>',
    lMail: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="3" y="5" width="18" height="14" rx="2"/><path d="M3.5 7l8.5 6 8.5-6"/></svg>',
    lPin: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 21s-7-6.2-7-11a7 7 0 1 1 14 0c0 4.8-7 11-7 11z"/><circle cx="12" cy="10" r="2.5"/></svg>',
    lDrop: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3s6 6.5 6 11a6 6 0 0 1-12 0c0-4.5 6-11 6-11z"/></svg>',
    save: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 4v11M7.5 10.5L12 15l4.5-4.5M5 19h14"/></svg>'
  };
  var CREDIT_NAME = 'হাসিবুল হক';
  var CREDIT_URL = 'https://www.facebook.com/hasibulhoque3335';
  var BATCH = '১৪৪৭-৪৮ হিজরী ২০২৬-২০২৭ শিক্ষাবর্ষ তাকমীল ফিল হাদিস সমাপনী শিক্ষার্থীবৃন্দ';

  function esc(s) {
    return String(s == null ? '' : s).replace(/[&<>"']/g, function (c) {
      return { '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c];
    });
  }
  function clean(v) { v = String(v == null ? '' : v).trim(); return (v === '—' || v === '-') ? '' : v; }
  function localPhone(p) {
    var d = String(p || '').replace(/\D/g, '');
    if (d.length === 10 && d.charAt(0) === '1') d = '0' + d;   // Sheets may drop the leading 0
    return d;
  }
  function phones(v) {
    return String(v || '').split(/[,;\n]/).map(localPhone).filter(Boolean);
  }
  function waNumber(r) {
    var src = localPhone(r.whatsapp) || phones(r.phone)[0] || '';
    if (!src) return '';
    if (src.indexOf('880') === 0) return src;
    if (src.charAt(0) === '0') return '88' + src;
    return src;
  }
  function driveId(s) {
    s = String(s || '').trim();
    var m = s.match(/\/d\/([A-Za-z0-9_-]+)/) || s.match(/[?&]id=([A-Za-z0-9_-]+)/);
    if (m) return m[1];
    return /^[A-Za-z0-9_-]{20,}$/.test(s) ? s : '';
  }
  function photoUrl(s) {
    s = String(s || '').trim();
    var id = driveId(s);
    if (id) return 'https://lh3.googleusercontent.com/d/' + id;
    return /^https?:\/\//i.test(s) ? s : '';
  }
  function fbUrl(s) {
    s = clean(s);
    if (/^https?:\/\//i.test(s)) return s;
    return /^[A-Za-z0-9._-]+$/.test(s) ? 'https://www.facebook.com/' + s : '';
  }
  function validMail(s) { return /^[^@\s]+@[^@\s]+\.[^@\s]+$/.test(s); }

  function cssUrl(u) { return encodeURI(u).replace(/'/g, '%27').replace(/\(/g, '%28').replace(/\)/g, '%29'); }
  function act(href, svg, label, external) {
    if (!href) return '<a class="q disabled" href="#" aria-disabled="true"><span class="qi">' + svg + '</span><span class="ql">' + label + '</span></a>';
    return '<a class="q" href="' + esc(href) + '"' + (external ? ' target="_blank" rel="noopener"' : '') + '><span class="qi">' + svg + '</span><span class="ql">' + label + '</span></a>';
  }
  function row(svg, label, valueHtml, href) {
    var inner = '<span class="ri">' + svg + '</span><span class="rt">' + valueHtml + '</span>';
    return href ? '<a class="row" href="' + esc(href) + '" aria-label="' + label + '">' + inner + '</a>' : '<div class="row" aria-label="' + label + '">' + inner + '</div>';
  }
  function val(v) {
    return v ? '<span class="val">' + esc(v) + '</span>' : '<span class="val pending">যোগ করা হয়নি</span>';
  }
  function vEsc(s) { return String(s).replace(/\\/g, '\\\\').replace(/[,;]/g, function (c) { return '\\' + c; }).replace(/\r?\n/g, ' '); }
  function vcard(r) {
    var name = clean(r.name), ph = phones(r.phone), mail = clean(r.gmail), fb = fbUrl(r.facebook);
    var addr = [clean(r.village), clean(r.thana), clean(r.district)].filter(Boolean).join(', ');
    var L = ['BEGIN:VCARD', 'VERSION:3.0', 'FN:' + vEsc(name), 'N:' + vEsc(name) + ';;;;', 'ORG:তাকমীল ফিল হাদিস ২০২৬-২০২৭'];
    ph.forEach(function (p) { L.push('TEL;TYPE=CELL:' + p); });
    if (validMail(mail)) L.push('EMAIL:' + mail);
    if (fb) L.push('URL:' + fb);
    if (addr) L.push('ADR;TYPE=HOME:;;' + vEsc(addr) + ';;;;');
    L.push('END:VCARD');
    return L.join('\r\n');
  }
  function downloadCard(r) {
    var blob = new Blob([vcard(r)], { type: 'text/vcard;charset=utf-8' });
    var a = document.createElement('a');
    a.href = URL.createObjectURL(blob);
    a.download = 'contact-' + String(idNum(r.id)) + '.vcf';
    document.body.appendChild(a); a.click(); document.body.removeChild(a);
    setTimeout(function () { URL.revokeObjectURL(a.href); }, 4000);
  }

  function renderProfile(r) {
    var ph = phones(r.phone), tel = ph[0] || '';
    var wa = waNumber(r);
    var mail = clean(r.gmail), mailOk = validMail(mail);
    var fb = fbUrl(r.facebook);
    var addr = [clean(r.village), clean(r.thana), clean(r.district)].filter(Boolean).join(', ');
    var blood = clean(r.blood);
    var real = photoUrl(r.photo);
    var photo = real || AVATAR;
    var name = clean(r.name);
    var father = clean(r.father);

    return '<main class="profile">' +
      '<header class="top"><p class="batch">তাকমীল ফিল হাদিস • ১৪৪৭-৪৮ হিজরী</p></header>' +
      '<section class="panel">' +
        '<div class="avatar">' +
          (real ? '<div class="photo-bg" style="background-image:url(\'' + esc(cssUrl(real)) + '\')"></div>' : '') +
          '<img class="photo" src="' + esc(photo) + '" alt="' + esc(name) + '" onerror="this.onerror=null;this.src=\'' + AVATAR + '\'">' +
        '</div>' +
        '<h1 class="name">' + esc(name) + '</h1>' +
        (father ? '<p class="role">পিতা: ' + esc(father) + '</p>' : '<p class="role">শিক্ষার্থী</p>') +
        '<div class="info">' +
          row(SVG.lPhone, 'ফোন', val(ph.join(', ')), tel ? 'tel:' + tel : '') +
          row(SVG.lMail, 'জিমেইল', val(mail), mailOk ? 'mailto:' + mail : '') +
          row(SVG.lPin, 'ঠিকানা', val(addr), '') +
          row(SVG.lDrop, 'রক্তের গ্রুপ', blood ? '<span class="val">রক্তের গ্রুপ: <span class="blood">' + esc(blood) + '</span></span>' : val(''), '') +
        '</div>' +
        '<button type="button" class="save" id="savecard">' + SVG.save + 'কন্টাক্টে সেভ করুন</button>' +
        '<nav class="quick" aria-label="যোগাযোগ">' +
          act(tel ? 'tel:' + tel : '', SVG.call, 'কল', false) +
          act(wa ? 'https://wa.me/' + wa : '', SVG.wa, 'হোয়াটসঅ্যাপ', true) +
          act(fb, SVG.fb, 'ফেসবুক', true) +
          act(mailOk ? 'mailto:' + mail : '', SVG.mail, 'ইমেইল', false) +
        '</nav>' +
      '</section>' +
      '<footer class="foot"><p class="fb">' + BATCH + '</p><p class="credit">Created by <a href="' + esc(CREDIT_URL) + '" target="_blank" rel="noopener">Hasibul Hoque</a></p></footer>' +
    '</main>';
  }

  function parseCSV(text) {
    var rows = [], row = [], f = '', q = false, i, c;
    text = String(text).replace(/^\uFEFF/, '');
    for (i = 0; i < text.length; i++) {
      c = text.charAt(i);
      if (q) {
        if (c === '"') { if (text.charAt(i + 1) === '"') { f += '"'; i++; } else q = false; }
        else f += c;
      } else if (c === '"') q = true;
      else if (c === ',') { row.push(f); f = ''; }
      else if (c === '\n' || c === '\r') {
        if (c === '\r' && text.charAt(i + 1) === '\n') i++;
        row.push(f); f = ''; rows.push(row); row = [];
      } else f += c;
    }
    if (f !== '' || row.length) { row.push(f); rows.push(row); }
    return rows;
  }
  function rowsToObjects(rows) {
    if (!rows.length) return [];
    var head = rows[0].map(function (h) { return String(h).trim().toLowerCase(); });
    if (head.indexOf('id') < 0 || head.indexOf('name') < 0) return [];   // not our sheet (e.g. a login page)
    return rows.slice(1).map(function (r) {
      var o = {}; head.forEach(function (h, i) { o[h] = r[i] == null ? '' : r[i]; }); return o;
    }).filter(function (o) { return String(o.id).trim() !== '' && String(o.name).trim() !== ''; });
  }
  function sheetUrl() {
    var c = W.SITE_CONFIG || {};
    if (c.SHEET_CSV_URL) return c.SHEET_CSV_URL;
    if (!c.SHEET_ID) return '';
    var u = 'https://docs.google.com/spreadsheets/d/' + encodeURIComponent(c.SHEET_ID) + '/gviz/tq?tqx=out:csv';
    if (c.SHEET_NAME) u += '&sheet=' + encodeURIComponent(c.SHEET_NAME);
    return u;
  }
  function loadData() {
    var url = sheetUrl();
    var fallback = function () { return W.FALLBACK_DATA || []; };
    if (!url || typeof fetch === 'undefined') return Promise.resolve(fallback());
    var timeout = new Promise(function (_, rej) { setTimeout(rej, 7000); });
    var req = fetch(url, { cache: 'no-store' }).then(function (r) {
      if (!r.ok) throw new Error('http');
      return r.text();
    }).then(function (t) {
      var o = rowsToObjects(parseCSV(t));
      if (!o.length) throw new Error('empty');
      return o;
    });
    return Promise.race([req, timeout]).catch(fallback);
  }
  function idNum(v) { return parseInt(String(v).replace(/\D/g, ''), 10); }

  function renderIndex(list, q) {
    q = (q || '').trim().toLowerCase();
    return list.filter(function (r) { return !q || clean(r.name).toLowerCase().indexOf(q) >= 0 || String(idNum(r.id)) === q; })
      .map(function (r) {
        var n = idNum(r.id), sn = n < 10 ? '0' + n : String(n);
        return '<li><a href="' + sn + '.html"><span class="no">' + sn + '</span>' + esc(clean(r.name)) + '</a></li>';
      }).join('');
  }

  function run() {
    var app = document.getElementById('app');
    if (!app) return;
    loadData().then(function (list) {
      if (W.PAGE === 'index') {
        app.innerHTML = '<div class="idx"><h1>' + BATCH + '</h1><input id="q" type="search" placeholder="নাম বা ক্রমিক নং দিয়ে খুঁজুন"><ul id="list">' + renderIndex(list, '') + '</ul></div>';
        document.getElementById('q').addEventListener('input', function (e) {
          document.getElementById('list').innerHTML = renderIndex(list, e.target.value);
        });
        return;
      }
      var id = idNum(W.STUDENT_ID), rec = null;
      for (var i = 0; i < list.length; i++) if (idNum(list[i].id) === id) { rec = list[i]; break; }
      if (!rec) { app.innerHTML = '<div class="loading">এই ক্রমিক নম্বরের তথ্য পাওয়া যায়নি।</div>'; return; }
      document.title = clean(rec.name) + ' — শিক্ষার্থী পরিচিতি';
      app.innerHTML = renderProfile(rec);
      var sb = document.getElementById('savecard');
      if (sb) sb.addEventListener('click', function () { downloadCard(rec); });
    });
  }

  var API = { renderProfile: renderProfile, parseCSV: parseCSV, rowsToObjects: rowsToObjects, waNumber: waNumber, phones: phones, photoUrl: photoUrl, renderIndex: renderIndex };
  if (typeof module !== 'undefined' && module.exports) module.exports = API;
  if (typeof document !== 'undefined') run();
})();