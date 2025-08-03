# thulite-images-validation-test

## Description

A sample site for testing w3 validator against @thulite/images

## Summary

All images added using markdown fail w3 validator <https://github.com/validator/validator> validation.

## Test procedure

1. Set up a test site with an Markdown image in a blog post
   1. `npm create thulite@latest thulite-image-validation-test -- --template doks`
   2. `cd thulite-image-validation-test`
   3. `npm install`
   4. `hugo new content/blog/image-test-post/index.md`
   5. Add an image to the post directory. E.g.
      1. `cd content/blog/image-test-post`
      2. `wget https://www.route93.ca/wp-content/uploads/WyeMarsh2.jpg`
      3. `cd -`
   6. Edit the blog post
      1. `code content/blog/image-test-post/index.md`
      2. Set `draft: false`
      3. Add the image to the content section of `index.md`. E.g.
         - `![Wooden bench in the Wye Marsh Wildlife Centre](WyeMarsh2.jpg)`
   7. Refresh the site
      1. Press Ctrl-C (there seems to be an issue with the Hugo server v0.148.2 when
         adding new content)
      2. Restart the hugo server: `npm run dev`
   8. Browse to new post (`http://localhost:1313/blog/image-test-post/`)
   9. Observe the image is displayed
   10. Cancel the server (Ctrl-C)
   11. Build the site: `hugo --gc`
2. Obtain and install W3 Nu Validator
   1. Download the latest release from
      <https://github.com/validator/validator/releases>
      1. E.g. `wget https://github.com/validator/validator/releases/download/latest/vnu.jar`
   2. Ensure you have a recent-ish Java JRE (I use openjdk-17-jre from Debian 12 'Bookworm')
3. Use the Validator and observe the results
   1. Execute `java -jar ./vnu.jar --skip-non-html $(find public -name '*.html' | tr $'\n' ' ')`
