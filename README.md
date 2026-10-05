# Verdant domain retirement

Deploy this directory as a separate Vercel project using the **Other** framework preset and this directory as the project root. It has no build command or dependencies. The `vercel.json` catch-all route returns HTTP **410 Gone** for the homepage and every nested path. Do not configure an old-domain redirect in this project.

After deploying, attach both `verdantvolunteers.org` and `www.verdantvolunteers.org` to this project. In Vercel, make sure neither hostname is configured to redirect to the other or to Ravel; each should return 410 directly. Point their DNS records to the values shown by Vercel. Ensure production deployment protection does not challenge Googlebot, or it will not see the 410 response. Keep the existing MX, SPF, DKIM, and DMARC DNS records for the temporary email sender. Leave the domain registered and HTTPS certificates active.

Check both hosts after DNS and certificates settle:

```sh
curl -I https://verdantvolunteers.org/
curl -I https://verdantvolunteers.org/help/article/example
curl -I https://www.verdantvolunteers.org/
curl -I https://www.verdantvolunteers.org/help/article/example
```

Each response should be `410` without a `Location` header. Check the homepage and an old nested URL in Google Search Console's URL Inspection tool, then use Removals if faster temporary hiding is needed. Once both hosts return 410, remove old-domain redirects from the Ravel frontend configuration. Avoid `robots.txt` disallow rules: Google needs to crawl the 410 responses.