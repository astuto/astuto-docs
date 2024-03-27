---
sidebar_position: 4
slug: /custom-domain
---

# Custom Domain Configuration

You can configure a custom domain (e.g. `feedback.yoursite.com`) to access Astuto instead of the default `subdomain.astuto.io`.

Follow these instructions in order:

1. In your domain management website, add a DNS record of type CNAME pointing to `cname.astuto.io`. **Note**: point exactly to cname.astuto.io, not yoursubdomain.astuto.io!
2. In Astuto site settings, go to "General" and fill the "Custom domain" field with the chosen host name (e.g. `feedback.yoursite.com`). **Note**: just write the host name, without `https` or slashes.
3. Click "Save". Wait a few moments and you should be able to access Astuto from `feedback.yoursite.com`.

:::caution Follow the instructions in order

You must first add the DNS CNAME record, and only then add the custom domain to Astuto. Doing the other way around won't work!

:::