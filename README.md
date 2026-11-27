# X Works website

Static site for **xworksaero.com**: X Works LLC (test pilot consultancy) and the SkySix pre-flight planning app.

Plain HTML and CSS. No build step.

| File | Page |
| --- | --- |
| `index.html` | Home |
| `support.html` | Support (use as the App Store **Support URL**: `https://xworksaero.com/support.html`) |
| `privacy.html` | Privacy policy (use as the App Store **Privacy Policy URL**: `https://xworksaero.com/privacy.html`) |
| `404.html` | Not-found page (Cloudflare Pages serves it automatically) |

To preview locally: `python3 -m http.server` in this folder, then open http://localhost:8000.

## Before submitting SkySix to Apple

Update the "SkySix app" section of `privacy.html` to say what the app actually collects (for example location, account details, crash reports) and match it to the App Privacy answers in App Store Connect.

## Going live on Cloudflare (free)

### 1. Add the site to Cloudflare Pages
1. Sign in at https://dash.cloudflare.com and open **Compute** > **Workers & Pages**.
2. Click **Create application**. On the next screen, open the **Pages** tab (or click the small **Get started** link next to "Looking to deploy Pages?" at the bottom). Do not use the Workers option.
3. Choose **Import an existing Git repository**, authorise GitHub if asked, and pick `ejbvmi/X_Works_Aero`.
4. Production branch: `main`. Framework preset: **None**. Build command: leave empty. Build output directory: leave empty, or `/` (the pages sit at the top of the repository).
5. Click **Save and Deploy**. You get a working `*.pages.dev` address within a minute.

### 2. Move the domain's DNS to Cloudflare
1. In the Cloudflare dashboard, choose **Add a domain**, enter `xworksaero.com`, and pick the **Free** plan.
2. Cloudflare scans your existing GoDaddy DNS records. Check that any **MX** and **TXT** records (email) were copied before continuing.
3. Cloudflare shows two nameservers (like `xxx.ns.cloudflare.com`).
4. In GoDaddy: **My Products** > `xworksaero.com` > **DNS** > **Nameservers** > **Change Nameservers** > **I'll use my own nameservers**, and paste the two Cloudflare nameservers.
5. Wait for Cloudflare to email that the domain is active (usually under an hour, can take up to 24).

### 3. Attach the domain to the site
1. Back in **Workers & Pages**, open the project > **Custom domains** > **Set up a custom domain**.
2. Add `xworksaero.com`, then add `www.xworksaero.com` too.
3. Cloudflare creates the DNS records and the HTTPS certificate automatically.

After this, every change merged into `main` on GitHub goes live on its own.
