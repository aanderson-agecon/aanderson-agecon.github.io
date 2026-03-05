# Setting Up Your Quarto Website on GitHub Pages

This guide walks you from a fresh download of these files to a live website.
Estimated time: **30–45 minutes** (less if you've used GitHub before).

---

## Step 1: Install Quarto

1. Go to **https://quarto.org/docs/get-started/**
2. Download and install the version for your operating system (Windows/Mac)
3. Restart RStudio after installing

**Verify it worked:** Open the RStudio Terminal (Tools → Terminal → New Terminal) and type:
```
quarto --version
```
You should see a version number like `1.x.x`.

---

## Step 2: Create a GitHub Repository

1. Go to **https://github.com** and sign in (or create a free account)
2. Click the **+** icon → **New repository**
3. Name it: `yourusername.github.io`
   - *(Replace "yourusername" with your actual GitHub username)*
   - *(This special name tells GitHub to serve it as your main personal site)*
4. Set it to **Public**
5. **Do not** check "Add a README" (we'll add our own files)
6. Click **Create repository**
7. Copy the repository URL (looks like `https://github.com/yourusername/yourusername.github.io.git`)

---

## Step 3: Set Up Git in RStudio

If you haven't used Git with RStudio before:

1. Install Git from **https://git-scm.com/downloads**
2. Restart RStudio
3. Go to **Tools → Global Options → Git/SVN**
4. Make sure the Git executable path is filled in
5. In the RStudio Terminal, set your identity (one-time setup):

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

## Step 4: Open This Project in RStudio

1. Unzip the downloaded `quarto-website.zip` file to a folder of your choice
2. In RStudio: **File → New Project → Existing Directory**
3. Navigate to the unzipped folder and click **Open**
4. RStudio will recognize it as a Quarto project

---

## Step 5: Initialize Git and Connect to GitHub

In the RStudio **Terminal** (not Console), run these commands one at a time:

```bash
git init
git add .
git commit -m "Initial website commit"
git branch -M main
git remote add origin https://github.com/yourusername/yourusername.github.io.git
git push -u origin main
```

*(Replace the URL with the one you copied in Step 2)*

---

## Step 6: Enable GitHub Pages

1. On GitHub, go to your repository
2. Click **Settings** → scroll to **Pages** (in the left sidebar)
3. Under "Source", select **Deploy from a branch**
4. Branch: **main** · Folder: **/docs**
5. Click **Save**

GitHub will show you your live URL — something like:
`https://yourusername.github.io`

**It may take 1–5 minutes for the site to appear the first time.**

---

## Step 7: Render Your Site

Back in RStudio, render your site by running in the Terminal:

```bash
quarto render
```

This builds your site into the `/docs` folder (which is what GitHub Pages serves).

Then push the rendered files to GitHub:

```bash
git add .
git commit -m "Render site"
git push
```

Your live site should update within a minute or two.

---

## Everyday Workflow (After Setup)

Once everything is connected, your workflow is simple:

1. **Edit** any `.qmd` file in RStudio
2. **Preview** locally: `quarto preview` in the Terminal (opens a live browser preview)
3. When ready to publish: `quarto render` then `git add . && git commit -m "Update" && git push`

---

## Customizing Your Content

### Replacing placeholder text
Search for `[` in all files (Ctrl+Shift+F in RStudio) to find all placeholder brackets like
`[University Name]`, `[your email]`, etc. Replace with your real information.

### Adding your headshot
1. Create an `images/` folder in the project root
2. Save your photo as `images/headshot.jpg`
3. In `index.qmd`, replace the placeholder div with:
   ```html
   <img src="images/headshot.jpg" class="profile-photo" alt="Dr. Your Name">
   ```

### Adding your CV
Replace `cv.pdf` in the project root with your actual CV PDF (keep the same filename),
or update the link in `index.qmd` and `teaching.qmd` to point to your file.

### Writing a new blog post
1. Create a new folder: `blog/posts/YYYY-MM-DD-short-title/`
2. Create `index.qmd` inside it
3. Copy the YAML header from an existing post and update the fields
4. Write your post — you can include R code chunks just like in R Markdown!

### Embedding R output in posts
Your blog posts are full Quarto documents. You can include R code chunks:

````markdown
```{r}
#| echo: false
library(tidyverse)
ggplot(mtcars, aes(mpg, wt)) + geom_point()
```
````

The output (charts, tables, etc.) renders automatically when you run `quarto render`.

---

## Useful Quarto Resources

- **Quarto website docs:** https://quarto.org/docs/websites/
- **Blog post format:** https://quarto.org/docs/websites/website-blog.html
- **R code in Quarto:** https://quarto.org/docs/computations/r.html
- **Custom theming:** https://quarto.org/docs/output-formats/html-themes.html

---

## Getting Help

If you run into issues:

- **Quarto GitHub Discussions:** https://github.com/quarto-dev/quarto-cli/discussions
- **Posit Community (RStudio forum):** https://community.rstudio.com
- The error messages from `quarto render` are usually quite descriptive — read them carefully!
