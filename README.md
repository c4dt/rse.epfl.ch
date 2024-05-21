# Research Software Engineers at EPFL

This is the repo for the RSE meetings at [EPFL](https://epfl.ch).
The URL for the website is:

[rse.epfl.ch](https://rse.epfl.ch)

Currently, there is no automatic deployment of the page.
You need to create a PR, and once it's merged, you need to push
it to

sftp://ic-ftps.epfl.ch

Access control is done using the EPFL group

https://groups.epfl.ch/#/home/S34249

Ask [Linus](linus.gasser@epfl.ch) if you want to participate in
the deployment of the site.

## Using the submodules

This repo uses `git submodule` for the template.
As much as I dislike git submodules, hugo proposes to do it that way.
If you're using devbox, the submodules will be installed automatically.
If you want to run hugo without devbox, install the submodules manually:

```bash
git submodule init
git submodule update
```

## Testing the page

To test, run the following:

```bash
devbox run server
```

## Adding a new blog

To add a new blog entry, run

```bash
devbox run hugo new content post/TITLE.md
```

replace `TITLE` with the title of your post.
Then you can edit [./content/post/TITLE.md] and watch the real-time update of the page
on http://localhost:1313

Once you're done, don't forget to set `draft = false`, else the blog will not show up
on the final page.

## Building the page

To build, run the following:

```bash
devbox run hugo
```

You will find the static html files in the [./public] directory.

## Deploying the page

To be able to deploy the page, you need to be part of the rse.epfl.ch group
at EPFL. Ask @ineiti, @PascalinDe, or @Lanterno to add you to the group.
Then you can set up rclone with the following config:
```toml
type = ftp
host = ic-ftps.epfl.ch
tls = false
explicit_tls = true
```

Use the following commands to do so:

```bash
devbox shell --pure
rclone config
```

Be sure to put `implicit_tls = false` and `explicit_tls = true`.

Then you can deploy using

```bash
devbox run update
```

This will pull the latest branch, run hugo, and copy the files over.
