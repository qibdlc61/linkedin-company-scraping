# linkedin company scraping: What Each Request Really Costs, Which Methods Risk Your Account, and How to Pull Company Data With a Plain API

Most people searching this want three things answered: what data you can actually get from a LinkedIn company page, which method won't put an account at risk, and what each company record costs once you scale past a spreadsheet. Short answers first. LinkedIn company pages are public and readable while logged out, so a proxy-based API that never touches your LinkedIn account is the lowest-risk route for company profiles. The catch is cost: on credit-based APIs, a LinkedIn page often doesn't cost 1 credit the way a normal site does — and that single multiplier changes your real per-company price by a large margin.

> **Quick picks**
> - Have a list of company URLs and want JSON in your own code? A proxy API fits. **ScraperAPI** routes requests through rotating proxies with no LinkedIn login, and the 7-day trial gives you 5,000 credits without a card. At LinkedIn's rate of 30 credits per request, that's roughly 166 company pages to validate field coverage. 👉 [Start the free ScraperAPI trial and run your own company list through it](https://www.scraperapi.com/pricing?fp_ref=coupons)
> - Need tens of thousands of records delivered in bulk? Per-record dataset vendors will be cheaper; details below.
> - Any tool asking for your LinkedIn cookie carries the actual ban risk. Company data alone rarely justifies it.

## What a LinkedIn company page actually gives you

The logged-out `/company/{name}/` page is the whole game for company scraping. It carries a JSON-LD `Organization` node plus an about section, and open-source scrapers on GitHub parse out roughly 13 fields from it: name, tagline, industry, company size, headquarters, founding year, specialties, website, follower count, and logo. The fact that hobbyist scripts and commercial APIs converge on the same field set tells you two useful things — the data is genuinely accessible without an account, and no vendor has secret extra company fields to offer.

What the public page does not contain matters just as much. Employee emails and phone numbers aren't there. Funding details top out at a yes/no "has venture financing" flag on some tools, with no round amounts or investor names. Employee lists and company posts sit behind separate endpoints or separate paid products on most platforms. One vendor's documentation says it plainly: fields depend on what the public page exposes, and a returned record is no guarantee every field will be present or accurate enough for downstream decisions.

There's also a field-level trap worth knowing before you trust any output. In one vendor's own published sample, Notion's record showed the size band "501-1,000 employees" alongside an `employeeCount` of 7,137 — the two numbers describe the same company and disagree badly. Size bands are self-reported on LinkedIn and drift out of date; if your pipeline needs headcount, treat the band and any numeric count as separate, unverified signals rather than audited figures.

## Three ways to scrape LinkedIn company data, and the one risk that actually matters

Method choice matters more than tool choice here, because the ban risk lives in how data is fetched, not in the data itself. Company pages are viewable logged out; the danger enters when your personal account gets involved.

| Method | How it runs | LinkedIn account needed | Main risk | Best fit |
| --- | --- | --- | --- | --- |
| Self-built script (Python + requests/BeautifulSoup) | Hits public pages or guest endpoints directly | No | IP bans and rate limits as volume grows | One-off pulls, learning, small jobs |
| Cookie-session browser tool | Vendor cloud runs with your logged-in cookie | Yes | Account restriction; often capped around 80 companies/day | Spreadsheet workflows, small recurring exports |
| Proxy API | Requests routed through rotating proxies to logged-out pages | No | Higher cost per request than plain sites | Recurring enrichment inside your own code |

The cookie row deserves emphasis. Handing your session to a third-party cloud is the most common cause of LinkedIn account restrictions, and the daily caps those tools impose exist precisely because of it — at 80 companies a day, enriching 2,500 companies takes a month of calendar time. A proxy API sidesteps the account question entirely, which is why it's the default recommendation when the goal is company-level data in bulk. 👉 [See ScraperAPI's LinkedIn setup, which works without any LinkedIn login](https://www.scraperapi.com/solutions/linkedin-scraper/?fp_ref=coupons)

For completeness: LinkedIn's official APIs for marketing and talent data require partner approval and can't be used to fetch arbitrary public company pages, which is why most teams end up choosing between the three routes above rather than "just using the official API."

## ScraperAPI plans and prices: the full lineup

ScraperAPI prices by credits, with seven tiers plus a free plan. Every paid plan includes JS rendering, premium proxies, auto-parsing, CAPTCHA handling, automatic retries, unlimited bandwidth, and a 99.9% uptime guarantee. Annual billing takes 10% off every tier, and the free plan gives 1,000 credits (5 concurrent connections) with no card required.

| Plan | Price (monthly / billed annually) | Credits per month | Concurrent threads | Get it |
| --- | --- | --- | --- | --- |
| Free | $0 | 1,000 | 5 | [Get 1,000 free credits](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Hobby | $49 / $44.10 | 100,000 | 20 | [View Hobby and start](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | $149 / $134.10 | 1,000,000 | 50 | [View Startup and start](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | $299 / $269.10 | 3,000,000 | 100 | [View Business and start](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | $475 / $427.50 | 5,000,000 | 200 | [View Scaling and start](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | $975 / $877.50 | 10,500,000 | 300 | [View Professional and start](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | $1,975 / $1,777.50 | 21,500,000 | 500 | [View Advanced and start](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom | 22,000,000+ | 500+ | [Contact sales for custom pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |

Secondary differences worth a second table, since they only show up after checkout:

| Feature | Hobby / Startup | Business and above |
| --- | --- | --- |
| Geotargeting | US & EU only | Country-level |
| Analytics dashboard history | Last 30 days | Unlimited |

### What a LinkedIn request actually costs on these plans

Here's the detail most comparison posts skip. ScraperAPI's pricing page states that one credit equals a standard page request, but harder sites are priced differently: Amazon costs 5 credits, Google and Bing cost 25, and **LinkedIn costs 30 credits per request**. Sites behind Cloudflare, Datadome, or PerimeterX add another 10 credits when bypassed.

Run that multiplier through the plan table and the real prices look like this:

- **Hobby** ($49): 100,000 ÷ 30 ≈ 3,333 LinkedIn requests ≈ **$14.70 per 1,000 companies**
- **Business** ($299): 3,000,000 ÷ 30 = 100,000 requests ≈ **$2.99 per 1,000**
- **Scaling** ($475): ≈ 166,666 requests ≈ **$2.85 per 1,000**
- **Advanced** ($1,975): ≈ 716,666 requests ≈ **$2.76 per 1,000**

Two practical takeaways. First, the 5,000-credit trial translates to about 166 LinkedIn pages — enough to check field coverage on a real sample, but budget it deliberately; a few 1-credit plain-site requests stretch the trial further while you explore. Second, Hobby is fine for proofs of concept but gets expensive per record fast; somewhere past a couple thousand companies a month, Business is where the per-record cost lands in the same territory as dedicated scrapers. 👉 [Check the current credit rates and plan prices on ScraperAPI's pricing page](https://www.scraperapi.com/pricing?fp_ref=coupons)

Before running any batch, two built-in guards are worth using: the dashboard's Domain Cost Estimator shows the exact credit cost for any URL before you spend anything, and a `max_cost` parameter caps what a single request may consume. Together they prevent the classic surprise-bill scenario on a 30-credit domain.

## How that compares with dedicated LinkedIn company scrapers

For context, here are verified prices from dedicated tools, checked as of October 2026. Credit, record, execution hour, and Actor run are different billing units, so treat these as rough anchors, not exact equivalents:

| Tool | Pricing model | Approx. cost | LinkedIn cookie needed |
| --- | --- | --- | --- |
| Bright Data | Pay per record | ~$1.50 per 1,000 records | No |
| ScrapeCreators | Credits ($10 / 5,000) | ~$2 per 1,000 company requests | No |
| Apify HarvestAPI actor | Per Actor | Listed between $3–4 per 1,000 (the platform's list page and README disagreed at time of check) | No |
| Apify curious_coder actor | $30/month rent + usage | Varies by run | Yes |
| PhantomBuster | Subscription | ~$56/month for 20 execution hours | Yes |
| Browse AI | Credits | Free 50 credits/month; Personal ~$19/month (annual) | No |
| MagicalAPI | Credits | $5 per 1,000 credits | No |

ScraperAPI sits between the groups. At mid-tier plans its per-record cost is comparable to dedicated no-cookie scrapers while also covering Google, Amazon, and everything else you scrape through one API. At entry tier it's pricier per record than raw dataset vendors — the honest trade-off for general-purpose flexibility. If your volume runs into tens of thousands of records every month and LinkedIn company data is all you need, a per-record vendor will win on price. If you're a developer enriching hundreds to a few thousand companies inside your own application, one API that handles every target tends to beat maintaining a separate vendor per site.

## How to pull a company page with ScraperAPI

The mechanics take minutes. You prefix the target URL with the ScraperAPI endpoint, and the service handles IP rotation, headers, and CAPTCHAs:

1. Sign up and grab your API key from the dashboard.
2. Request `http://api.scraperapi.com?api_key=YOUR_KEY&url=https://www.linkedin.com/company/notion/`. For stubborn targets, add `ultra_premium=true` to route through the highest-grade proxy pool.
3. Parse the HTML. Company pages embed the JSON-LD `Organization` node with `industry`, `company_size`, `headquarters`, `founded`, and `specialties`; standard libraries cover this — `requests` for the call, Beautiful Soup for parsing. No headless browser needed, since the data sits in the initial HTML.
4. Export one JSON record per company to CSV or push it straight into your CRM.

If your project extends to job listings, the same proxy prefix works on LinkedIn's guest jobs endpoint. The official tutorial documents the pagination quirk: the jobs search uses infinite scroll, the internal `seeMoreJobPostings/search` API takes a `start` parameter that increments by 25 per page, and the current last page is start=975 — hitting 1000 returns a 404. Knowing that boundary saves you from scraping phantom pages.

## Limits to know before you buy

Three constraints from the plan structure only surface after checkout, so here they are up front.

**Geotargeting is tier-gated.** Hobby and Startup route requests through US and EU locations only; country-level geotargeting starts at Business. This matters for LinkedIn more than for most sites, because company pages and job results vary by region. If your targets sit outside the US and EU, start at Business.

**Concurrency is capped, not queued.** Exceed your plan's thread limit and you get a 429 response — the request is turned away and you simply retry, with no extra charge. Hobby's 20 threads versus Scaling's 200 is the difference between minutes and hours on a 3,000-company batch.

**Running dry pauses you by default.** When credits run out, scraping stops until renewal rather than silently overbilling. Hobby through Professional can opt into auto-upgrade to the next tier; Scaling and above can enable pay-as-you-go at a fixed per-credit rate with a monthly cap you set. If your monthly volume is unpredictable, that toggle decides whether a batch job finishes or stalls halfway.

## FAQ

**Is scraping public LinkedIn company data legal?** Public company pages are viewable while logged out, and that's the layer proxy APIs access. LinkedIn's official APIs for company and talent data require partner approval, which is why scraping fills the gap for arbitrary pages. Company-level public info is the lowest-risk category; employee personal profiles are a different, stricter matter, and privacy rules like GDPR apply to how you store and use any personal data. This isn't legal advice.

**Do I need a LinkedIn account or cookie?** Not with ScraperAPI — requests go through rotating proxies to logged-out pages. That's the core advantage over cookie-session automation tools, and it's also why there's no daily company cap of the "80 per day" variety.

**How many companies can I test for free?** The 7-day trial includes 5,000 credits, about 166 LinkedIn page requests at the 30-credit rate. Enough to validate field coverage on a genuine sample of your list before paying anything.

**What happens when a request fails?** CAPTCHAs and retries are handled automatically by the proxy layer, and the analytics dashboard shows per-request outcomes so you can see what's actually being returned.

## Choosing fast

Enriching a few hundred to a few thousand companies per month from your own code, with zero interest in risking a LinkedIn account: ScraperAPI's Business plan at $299/month works out to about $2.99 per 1,000 LinkedIn pages, and the free trial settles the field-coverage question in a day. Tens of thousands of records monthly, LinkedIn-only, no need for a general API: a per-record dataset vendor costs less. Someone offering you a tool that needs your LinkedIn cookie for company pages: the daily caps and account exposure are hard to justify for data that's public anyway. Before checkout, two things to confirm: your target regions (they decide whether Business is your real entry point) and your monthly volume (it decides Hobby versus Business versus Scaling). 👉 [Start with ScraperAPI's free 5,000-credit trial and test it on your own company list](https://www.scraperapi.com/pricing?fp_ref=coupons)
