# Word of Life — Site Maintenance Guide

This README explains how to add new **Books**, **English Articles**, and **Malayalam Articles** to `index.html`. All content lives inside a single file — there is no build step. Just edit `index.html`, commit, and push to GitHub.

---

## 1. Repository layout

```
word-of-life/
├── index.html                ← the page you edit
├── assets/
│   └── img/
│       ├── logo.webp
│       ├── cover_eBook_*.webp        ← book covers   (600 × 900 px)
│       └── cover_article_*.webp      ← article covers (600 × 900 px)
└── books/
    ├── eBook_*.pdf                   ← book PDFs
    ├── article_*_en.html             ← English article pages
    └── article_*_mal.html            ← Malayalam article pages
```

**Before adding any card, upload two files first:**

1. The **cover image** → `assets/img/` (WebP, exactly **600 × 900 px**).
2. The **content file** → `books/` (a `.pdf` for books, `.html` for articles).

Use lowercase, no-spaces filenames (`my_new_book.pdf`, not `My New Book.pdf`).

---

## 2. How the page is organised

Inside `index.html` there is one container:

```html
<div class="grid" id="grid">
   ... all cards live here ...
</div>
```

Each card is one `<article>` block. The **`data-cat`** attribute decides which tab it appears under:

| Tab on the page          | `data-cat` value   |
|--------------------------|--------------------|
| Books                    | `books`            |
| Articles (EN)            | `articles-en`      |
| ലേഖനങ്ങൾ (Malayalam)  | `articles-mal`     |

The **`data-title`** attribute is what the search box matches against. Put every keyword (English transliteration **and** topic words) in there, all lowercase.

The tab counters (e.g. `Books 5`) update automatically — you do **not** edit them.

---

## 3. Adding a new BOOK

Find the comment `<!-- ============ BOOKS ============ -->` in `index.html` and paste a new block just below the last existing book card.

### Template — English book

```html
<article class="card" data-cat="books" data-title="SEARCH KEYWORDS HERE LOWERCASE">
  <a href="./books/FILENAME.pdf" class="cover-wrap" title="BOOK TITLE">
    <span class="lang-pill">English</span>
    <img src="./assets/img/COVER.webp"
         alt="BOOK TITLE — book cover"
         loading="lazy" width="600" height="900">
  </a>
  <div class="card-body">
    <h3 class="card-title">BOOK TITLE</h3>
    <p class="card-meta">Book · PDF · SIZE</p>
    <a href="./books/FILENAME.pdf" class="read-link">Read online</a>
  </div>
</article>
```

### Template — Malayalam book

Three changes vs. the English template:

1. `<span class="lang-pill">മലയാളം</span>`
2. Add the `mal` class on the title: `<h3 class="card-title mal">...</h3>`
3. Read link label: `വായിക്കുക` instead of `Read online`

```html
<article class="card" data-cat="books" data-title="transliteration keywords malayalam">
  <a href="./books/FILENAME.pdf" class="cover-wrap" title="ENGLISH TITLE — Malayalam">
    <span class="lang-pill">മലയാളം</span>
    <img src="./assets/img/COVER.webp"
         alt="MALAYALAM TITLE — book cover"
         loading="lazy" width="600" height="900">
  </a>
  <div class="card-body">
    <h3 class="card-title mal">മലയാളം ടൈറ്റിൽ</h3>
    <p class="card-meta">Book · PDF · SIZE</p>
    <a href="./books/FILENAME.pdf" class="read-link">വായിക്കുക</a>
  </div>
</article>
```

**Tip — file size:** right-click the PDF → *Properties* (or `ls -lh`) and round, e.g. `493 KB`, `1.2 MB`.

---

## 4. Adding a new ARTICLE — English

Find `<!-- ============ ARTICLES — ENGLISH ============ -->` and paste below the last English article.

```html
<article class="card" data-cat="articles-en" data-title="search keywords lowercase">
  <a href="./books/article_SLUG_en.html" class="cover-wrap" title="ARTICLE TITLE">
    <span class="lang-pill">English</span>
    <img src="./assets/img/cover_article_SLUG.webp"
         alt="ARTICLE TITLE — cover"
         loading="lazy" width="600" height="900">
  </a>
  <div class="card-body">
    <h3 class="card-title">ARTICLE TITLE</h3>
    <p class="card-meta">Article · HTML</p>
    <a href="./books/article_SLUG_en.html" class="read-link">Read online</a>
  </div>
</article>
```

Key points:
- `data-cat="articles-en"` (this is what puts it in the English Articles tab).
- The link points to an `.html` file in `books/`.
- The card-meta usually reads `Article · HTML` (or `Article · PDF · SIZE` if you publish a PDF).

---

## 5. Adding a new ARTICLE — Malayalam

Find `<!-- ============ ARTICLES — MALAYALAM ============ -->` (or paste below the last `articles-mal` card) and use:

```html
<article class="card" data-cat="articles-mal" data-title="transliteration keywords malayalam">
  <a href="./books/article_SLUG_mal.html" class="cover-wrap" title="ENGLISH TITLE — Malayalam">
    <span class="lang-pill">മലയാളം</span>
    <img src="./assets/img/cover_article_SLUG_mal.webp"
         alt="MALAYALAM TITLE — cover"
         loading="lazy" width="600" height="900">
  </a>
  <div class="card-body">
    <h3 class="card-title mal">മലയാളം തലക്കെട്ട്</h3>
    <p class="card-meta">Article · HTML</p>
    <a href="./books/article_SLUG_mal.html" class="read-link">വായിക്കുക</a>
  </div>
</article>
```

Three Malayalam-specific differences (same as Malayalam books):
1. Language pill: `മലയാളം`
2. Title class includes `mal` → enables the Malayalam font.
3. Read link label: `വായിക്കുക`

---

## 6. Quick checklist before you commit

- [ ] Cover image uploaded to `assets/img/` and is **600 × 900 px WebP**.
- [ ] PDF or HTML file uploaded to `books/`.
- [ ] New `<article>` block pasted under the correct comment section.
- [ ] `data-cat` is one of `books`, `articles-en`, `articles-mal`.
- [ ] `data-title` is lowercase, includes English keywords (so search works for both languages).
- [ ] For Malayalam: `lang-pill` says `മലയാളം`, title has `mal` class, read link says `വായിക്കുക`.
- [ ] Both `href` values in the card (cover link + read link) point to the same file.

---

## 7. Publishing to GitHub Pages

From the repo folder:

```bash
git add index.html assets/img/COVER.webp books/FILENAME.pdf
git commit -m "Add: <title>"
git push
```

GitHub Pages will rebuild within a minute. Hard-refresh the page (`Ctrl/Cmd + Shift + R`) to bypass the browser cache.

---

## 8. Troubleshooting

| Symptom                                 | Fix                                                                 |
|----------------------------------------|---------------------------------------------------------------------|
| Card appears in **All** but not in its tab | `data-cat` value is misspelled — must be `books` / `articles-en` / `articles-mal`. |
| Cover image is blank or 404            | Check the `src` path and the actual filename — case-sensitive on GitHub. |
| Cover looks stretched or squished      | Image must be exactly **600 × 900 px**. Re-export and replace.      |
| Malayalam title shows as boxes / wrong font | Add the `mal` class on the `<h3>` (`class="card-title mal"`).   |
| Search doesn't find a new card         | Add more keywords (English transliteration + topic words) to `data-title`. |
| Tab counter didn't change              | Hard-refresh; the counter is recomputed every page load.            |
